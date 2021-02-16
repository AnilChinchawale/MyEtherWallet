
<script>
import CustomerSupport from '@/components/CustomerSupport';
export default {
  components: {
    'customer-support': CustomerSupport
  },
  data() {
    return {
      faqs: {
        faq1: {
          open: false,
          title: 'home.faqs.mew-wallet.title',
          content: 'home.faqs.mew-wallet.text',
          linkText: 'home.faqs.button-learn-more',
          link:
            'https://kb.myetherwallet.com/en/mewwallet/mewwallet-user-guide/'
        },
        faq2: {
          open: false,
          title: 'home.faqs.other-wallets.title',
          content: 'home.faqs.other-wallets.text',
          linkText: 'home.faqs.button-here',
          link:
            'https://kb.myetherwallet.com/en/getting-started/how-to-access-your-wallet/'
        },
        faq3: {
          open: false,
          title: 'home.faqs.send-txs.title',
          content: 'home.faqs.send-txs.text',
          linkText: 'home.faqs.button-here',
          link:
            'https://kb.myetherwallet.com/en/transactions/how-to-send-a-transaction/'
        },
        faq4: {
          open: false,
          title: 'home.faqs.forgot-pwd.title',
          content: 'home.faqs.forgot-pwd.text',
          linkText: 'home.faqs.button-here',
          link:
            'https://kb.myetherwallet.com/en/security-and-privacy/lost-private-key/'
        },
        faq5: {
          open: false,
          title: 'home.faqs.create-wallet.title',
          content: 'home.faqs.create-wallet.text',
          linkText: 'home.faqs.button-here',
          link:
            'https://kb.myetherwallet.com/en/getting-started/how-to-create-a-wallet/'
        }
      }
    };
  },
  methods: {
    openFAQ: function (faqToOpen) {
      this.faqs[faqToOpen].open = !this.faqs[faqToOpen].open;
    }
  }
};
</script>

<style lang="scss" scoped>
@import 'FaqsContainer.scss';
</style>
