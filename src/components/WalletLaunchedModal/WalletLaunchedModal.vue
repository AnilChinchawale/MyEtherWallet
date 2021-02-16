

<script>
import appStore from '@/assets/images/icons/button-app-store.png';
import googlePlay from '@/assets/images/icons/button-google-play-color.png';

export default {
  data() {
    return {
      storeButtons: [
        {
          src: appStore,
          url: 'https://itunes.apple.com/app/id1464614025'
        },
        {
          src: googlePlay,
          url:
            'https://play.google.com/store/apps/details?id=com.myetherwallet.mewwallet'
        }
      ]
    };
  },
  methods: {
    closeModal() {
      this.$refs.walletLaunch.hide();
    }
  }
};
</script>

<style lang="scss">
@import 'WalletLaunchedModal.scss';

.wallet-launch-modal {
  .modal-body {
    padding: 0;
  }
  .modal-dialog {
    max-width: 820px;
  }
}

@media screen and (max-width: 820px) {
  .wallet-launch-modal {
    .modal-dialog {
      max-width: 500px !important;
    }
  }
}
</style>
