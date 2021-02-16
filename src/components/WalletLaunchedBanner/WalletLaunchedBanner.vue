

<script>
import appStore from '@/assets/images/icons/button-app-store.png';
import googlePlay from '@/assets/images/icons/button-google-play-color.png';
import store from 'store';

export default {
  data() {
    return {
      hideBanner: false,
      isExpanded: false,
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
  mounted() {
    this.hideBanner = store.get('hideBanner');
  },
  methods: {
    toggleBanner() {
      this.isExpanded = !this.isExpanded;
    },
    setHideBanner() {
      this.hideBanner = true;
      store.set('hideBanner', true);
    }
  }
};
</script>

<style lang="scss">
@import 'WalletLaunchedBanner.scss';
</style>
