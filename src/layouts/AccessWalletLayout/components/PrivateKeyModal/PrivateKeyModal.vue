<template>
  <b-modal
    ref="privateKey"
    :title="$t('accessWallet.private-key.modal.title')"
    hide-footer
    class="bootstrap-modal nopadding modal-software"
    centered
    static
    lazy
    @shown="focusInput"
    @hide="privateKey = ''"
  >
    <div class="modal-content-block">
      <div class="private-key-form">
        <div class="input-container">
          <input
            ref="privateKeyInput"
            v-model="privateKey"
            :placeholder="$t('accessWallet.private-key.modal.placeholder')"
            type="text"
            name="PrivateKey"
            autocomplete="off"
            @keypress.enter="unlockWallet"
          />
        </div>
        <standard-button
          :button-disabled="notValid"
          :options="{
            title: $t('common.wallet.access'),
            buttonStyle: 'green',
            noMinWidth: true
          }"
          :click-function="unlockWallet"
          class="submit-button"
        />
      </div>
      <div class="customer-support-block">
        <!-- <customer-support /> -->
      </div>
    </div>
  </b-modal>
</template>

<script>
import { WalletInterface } from '@/wallets';
import { PRIV_KEY as privKeyType } from '@/wallets/bip44/walletTypes';
import { mapState, mapActions } from 'vuex';
import { isHexString } from 'ethereumjs-util';
import StandardButton from '@/components/Buttons/StandardButton';
import { Toast } from '@/helpers';

export default {
  components: {
    'standard-button': StandardButton
  },
  data() {
    return {
      privateKey: '',
      spinner: false
    };
  },
  computed: {
    ...mapState('main', ['path']),
    notValid() {
      const _priv = this.privateKey.replace('0x', '');
      return !isHexString('0x' + _priv, 32);
    },
    actualPrivKey() {
      return this.privateKey.substr(0, 2) === '0x'
        ? this.privateKey.replace('0x', '')
        : this.privateKey;
    }
  },
  methods: {
    ...mapActions('main', ['decryptWallet']),
    unlockWallet() {
      try {
        const walletInstance = new WalletInterface(
          this.actualPrivKey,
          false,
          privKeyType
        );
        this.spinner = true;
        this.decryptWallet([walletInstance]).then(() => {
          this.spinner = false;
          this.$router.push({
            path: 'interface'
          });
        });
      } catch (e) {
        Toast.responseHandler(
          `${this.$i18n.t('common.invalid-private-key')}`,
          Toast.WARN
        );
      }
    },
    focusInput() {
      this.$refs.privateKeyInput.focus();
    }
  }
};
</script>
<style lang="scss" scoped>
@import 'PrivateKeyModal-desktop.scss';
@import 'PrivateKeyModal-tablet.scss';
@import 'PrivateKeyModal-mobile.scss';
</style>
