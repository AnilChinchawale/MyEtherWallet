<template>
  <b-modal
    ref="software"
    :title="$t('accessWallet.software.modal.title')"
    hide-footer
    class="bootstrap-modal nopadding modal-software"
    centered
    static
    lazy
  >
    <div class="content-block">
      <div class="d-block content-container text-center">
        <div class="button-options">
          <wallet-option
            v-for="(item, idx) in items"
            :key="item.name + idx"
            :selected="selected === item.name"
            :hover-icon="item.imgHoverPath"
            :text="$t(item.text)"
            :name="item.name"
            @updateSelected="updateSelected"
          />
        </div>
        <input
          ref="jsonInput"
          type="file"
          name="file"
          style="display: none"
          @change="uploadFile"
        />
      </div>
      <div class="button-container-block">
        <standard-button
          :button-disabled="selected !== '' ? false : true"
          :options="{
            title: $t('common.continue'),
            buttonStyle: 'green',
            noMinWidth: true,
            fullWidth: true
          }"
          :click-function="continueAccess"
        />
      </div>
      <!-- <customer-support /> -->
    </div>
  </b-modal>
</template>

<script>
import byJsonImgHov from '@/assets/images/icons/button-json-hover.svg';
import byMnemImgHov from '@/assets/images/icons/button-mnemonic-hover.svg';
import privKeyImgHov from '@/assets/images/icons/button-key-hover.svg';
import WalletOption from '../WalletOption';
import StandardButton from '@/components/Buttons/StandardButton';
import { Toast } from '@/helpers';

export default {
  components: {
    'wallet-option': WalletOption,
    'standard-button': StandardButton
  },
  props: {
    value: {
      type: String,
      default: ''
    },
    openPassword: {
      type: Function,
      default: function () {}
    },
    openMnemonicPhraseInput: {
      type: Function,
      default: function () {}
    },
    openPrivateKeyInput: {
      type: Function,
      default: function () {}
    }
  },
  data() {
    return {
      file: '',
      selected: '',
      items: [
        {
          name: 'byJson',
          imgHoverPath: byJsonImgHov,
          text: 'accessWallet.json-file'
        },
        {
          name: 'byMnem',
          imgHoverPath: byMnemImgHov,
          text: 'accessWallet.mnemonic.string'
        },
        {
          name: 'byPriv',
          imgHoverPath: privKeyImgHov,
          text: 'accessWallet.private-key.string'
        }
      ]
    };
  },
  methods: {
    uploadClick() {
      const jsonInput = this.$refs.jsonInput;
      jsonInput.value = '';
      jsonInput.click();
    },
    continueAccess() {
      if (this.selected === 'byJson') {
        this.uploadClick();
      } else if (this.selected === 'byPriv') {
        this.openPrivateKeyInput();
      } else if (this.selected === 'byMnem') {
        this.openMnemonicPhraseInput();
      }
    },
    updateSelected(ref) {
      if (this.selected !== ref) {
        this.selected = ref;
      } else {
        this.selected = '';
      }
    },
    select(ref) {
      if (this.selected !== ref) {
        this.selected = ref;
      } else {
        this.selected = '';
      }
    },
    uploadFile(e) {
      const self = this;
      const reader = new FileReader();
      reader.onloadend = function (evt) {
        try {
          self.$emit('file', JSON.parse(evt.target.result));
          self.file = JSON.parse(evt.target.result);
        } catch (e) {
          Toast.responseHandler(e, Toast.ERROR);
        }
      };
      reader.readAsBinaryString(e.target.files[0]);
    }
  }
};
</script>

<style lang="scss" scoped>
@import 'SoftwareModal-desktop.scss';
@import 'SoftwareModal-tablet.scss';
@import 'SoftwareModal-mobile.scss';
</style>
