<template lang='pug'>
modal-base-template(class='has-background')
  .wrapper-container
    tab-wrapper(:tabNav='settings')
      tab-item
        user-profile
      tab-item
        tab-placeholder(name='Privacy & Safety')
      tab-item
        tab-placeholder(name='Notifications')
      tab-item
        appearence
      tab-item
        tab-placeholder(name='Changelog')
</template>

<script>
import Settings from '~/frontend/model/settings.js'
import ModalBaseTemplate from '@components/Modal/ModalBaseTemplate.vue'
import TabItem from '@components/Tabs/TabItems.vue'
import TabWrapper from '@components/Tabs/TabWrapper.vue'
import TabPlaceholder from './Placeholder.vue'
import Appearence from './Appearence.vue'
import UserProfile from './UserProfile.vue'

export default {
  name: 'SettingsWrapper',

  components: {
    ModalBaseTemplate,
    TabWrapper,
    TabItem,
    Appearence,
    UserProfile,
    TabPlaceholder
  },

  data () {
    return Settings
  }
}
</script>

<style lang='scss' scoped>
@import "../../../assets/style/_variables.scss";

.wrapper-container {
  height: 100%;
  width: 100%;
  opacity: 1;
}

.settings-container {
  position: relative;
  margin: 0 26px;
  max-width: 620px;
}
</style>
