<!-- @format -->

<template>
  <div id="nav">
    <span class="logo heading">
      Africa Tech Response
    </span>

    <span class="icons">
      <a-icon type="reload" :rotate="270" @click="refresh()" />
      <a-icon type="info-circle" />
    </span>
  </div>
</template>

<script>
  import EventBus from '../eventbus'
  export default {
    methods: {
      refresh() {
        this.$confirm({
          title: 'Are you sure restart this test?',
          content: 'This action is irreversible.',
          okText: 'Yes',
          okType: 'danger',
          cancelText: 'No',
          onOk: () => {
            console.log('OK')
            this.$route.name !== 'Welcome' ? this.$router.push('/') : EventBus.$emit('refresh')
            this.$store.commit('clear_data', null)
          },
          onCancel: () => {
            console.log('Cancel')
          },
        })
      },
    },
  }
</script>
