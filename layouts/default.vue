<template>
  <div
    class="
      relative
      flex flex-col
      w-full
      font-sans
      antialiased
      text-gray-800
      bg-gray-100
    "
  >
    <div class="min-h-screen">
      <div
        v-if="!store.id && settings.isMultiStore"
        class="
          px-8
          py-12
          flex flex-col
          min-h-screen
          items-center
          justify-center
        "
      >
        <div
          class="mb-6 text-2xl font-bold text-center text-gray-800 md:text-3xl"
        >
          <img src="/no/dog-png-1.png" alt="" class="mx-auto h-96 w-72" />
          <p>Oops! Store not found</p>
        </div>

        <a :href="`${settings.ADMIN_PANEL_LINK}`" class="mb-5">
          <PrimaryButtonRounded class="w-52">
            Create your store
          </PrimaryButtonRounded>
        </a>

        <div class="mb-1 text-xs font-semibold text-center">
          {{ settings.websiteName }}
        </div>
      </div>

      <div v-else>
        <NavLanding class="fixed top-0 z-50 w-full" @showLogin="showLogin" />
        <div :class="settings.id ? 'mt-rem' : 'mt-noSettingID'">
          <Nuxt class="w-full" />
        </div>
      </div>
    </div>

    <WhiteFooter class="hidden sm:block" />

    <OtpLogin v-if="showLoginModal" @showLogin="showLogin" />

    <Modal :show="store.closed" title="Store is not accepting orders now">
      {{ store.closedMessage || 'Please visit back later' }}
    </Modal>
  </div>
</template>
<script>
import OtpLogin from '~/components/Login/Mobile/OtpLogin.vue'
import NavLanding from '~/components/Home/NavLanding.vue'
import WhiteFooter from '~/components/Island/WhiteFooter.vue'
import { Modal } from '~/shared/components/ui'
import PrimaryButtonRounded from '~/components/ui/PrimaryButtonRounded.vue'
export default {
  components: {
    NavLanding,
    OtpLogin,
    WhiteFooter,
    Modal,
    PrimaryButtonRounded,
  },
  data() {
    return {
      showLoginModal: false,
      loading: false,
    }
  },
  head() {
    return this.$nuxtI18nHead()
  },
  computed: {
    settings() {
      return this.$store.state.settings || {}
    },
    store() {
      return this.$store.state.store || {}
    },
  },
  methods: {
    showLogin(e) {
      this.showLoginModal = e
    },
  },
}
</script>

<style scoped>
@media (max-width: 1024px) {
  .mt-rem {
    margin-top: 4.55rem;
  }
}
@media (min-width: 1024px) {
  .mt-rem {
    margin-top: 5.7rem;
  }
}
@media (max-width: 1024px) {
  .mt-noSettingID {
    margin-top: 6.7rem;
  }
}
@media (min-width: 1024px) {
  .mt-noSettingID {
    margin-top: 7.6rem;
  }
}
</style>
