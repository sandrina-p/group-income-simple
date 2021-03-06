<template lang='pug'>
div
  i18n.steps-title(tag='p') 1. Create a new group

  label.avatar(for='groupPicture')
    //- TODO: set a default placeholder image using a built-in asset
    avatar(ref='picture')
    //- we don't need to add any code to trigger the hidden file input field
    //- because we use this label(for='elem') trick:
    //- https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications#Using_a_label_element_to_trigger_a_hidden_file_input_element
    i18n.link Upload an image

    input.groupPictureInput#groupPicture(
      type='file'
      name='groupPicture'
      accept='image/*'
      :class='{error: v.groupPicture.$error}'
      @change='fileChange($event.target.files)'
      placeholder='http://'
      data-test='groupPicture'
    )

  i18n.error(v-if='v.groupPicture.$error' tag='p') The group picture must be a valid url

  i18n.label(tag='label') What is the name of your group?

  input.input.is-large.is-primary(
    ref='name'
    type='text'
    name='groupName'
    :class='{ error: v.groupName.$error }'
    :value='group.groupName'
    @input='update'
    @keyup.enter='next'
    data-test='groupName'
  )
</template>

<script>
import Avatar from '@components/Avatar.vue'

export default {
  name: 'GroupName',
  props: {
    group: { type: Object },
    v: { type: Object }
  },
  inject: ['$assistant'],
  components: {
    Avatar
  },
  mounted () {
    this.$refs.name.focus()
  },
  methods: {
    update (e) {
      this.v.groupName.$touch()
      this.$emit('input', {
        data: {
          groupName: e.target.value
        }
      })
    },
    next (e) {
      this.v[e.target.name].$touch()
      if (!this.v[e.target.name].$invalid) {
        this.$emit('next')
      }
    },
    fileChange (files) {
      if (!files.length) return
      this.v.groupPicture.$touch()
      this.$assistant.ephemeral.groupPictureFile = files[0]
      this.$refs.picture.setFromBlob(files[0])
    }
  }
}
</script>

<style lang='scss' scoped>
@import "../../../assets/style/_variables.scss";

.username {
  display: none;
  margin-bottom: $spacer-lg;
  color: $text_1;

  @include tablet {
    display: block;
  }
}

.avatar {
  height: 125px;
  margin: 40px auto 32px auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;

  .c-avatar {
    width: 95px;
    height: 95px;
  }

  .link {
    display: inline-block;
    margin-top: 7px;

    @include tablet {
      display: block;
      margin-top: 0;
    }
  }

  img {
    display: block;
    width: 113px;
    height: 113px;
    margin: 0 auto;

    @include tablet {
      width: 71px;
      height: 71px;
    }
  }
}

.groupPictureInput {
  display: none;
}
</style>
