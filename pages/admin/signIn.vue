<template>
  <div
    id="admin"
    :class="displayStatusStore.displaySize"
  >
    <div class="title">
      <Button
        fit-content
        color="transparent"
        icon="chevron_left"
        @click="navigateTo('/')"
      >
        Back to top
      </Button>
      <h1>
        This is
        <HighLight>
          admin
        </HighLight>
        page
      </h1>
      <p>You must be logged in with an authorized account to access this page</p>
      <hr>
      <div class="buttons">
        <SignInButton provider="github" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
/* -- type, interface -- */

/* -- store -- */
const userDataStore = useUserDataStore()
const colorStore = useColorStore()
const displayStatusStore = useDisplayStatusStore()

/* -- props, emit -- */

/* -- variable(ref, reactive, computed) -- */

/* -- function -- */

/* -- watch -- */

/* -- life cycle -- */
onBeforeMount(() => {
  if (userDataStore.supabaseUser?.id) {
    navigateTo('/admin')
  }
})

watch(userDataStore.supabaseUser!, (newVal) => {
  if (newVal.id) {
    navigateTo('/admin')
  }
})

definePageMeta({
  title: 'Admin SignIn'
})
</script>

<style lang="scss" scoped>
#admin {
  display: grid;
  align-items: center;
  justify-content: start;

  height: 100%;

  p {
    color: v-bind("colorStore.color.theme.subText");
  }

  hr {
    margin: 1rem 0px;
  }

  .buttons {
    display: flex;
    flex-flow: column;

    #Button {
      padding: 0px;
      margin-top: 1rem;
    }
  }

  &.pc {

  }

  &.lp {

  }

  &.sm {

  }
}
</style>
