<script setup lang="ts">
import type { FormError, FormSubmitEvent } from '#ui/types'

const fileRef = ref<{ input: HTMLInputElement }>()
const isDeleteAccountModalOpen = ref(false)

const state = reactive({
  name: 'TabooGenerate',
  package: 'com.github.taboo.generate',
  username: 'benjamincanac',
  avatar: '',
  bio: '',
  password_current: '',
  password_new: ''
})

const toast = useToast()

function validate (state: any): FormError[] {
  const errors = []
  if (!state.name) errors.push({ path: 'name', message: 'Please enter your name.' })
  if (!state.email) errors.push({ path: 'email', message: 'Please enter your email.' })
  if ((state.password_current && !state.password_new) || (!state.password_current && state.password_new)) errors.push({ path: 'password', message: 'Please enter a valid password.' })
  return errors
}

function onFileChange (e: Event) {
  const input = e.target as HTMLInputElement

  if (!input.files?.length) {
    return
  }

  state.avatar = URL.createObjectURL(input.files[0])
}

function onFileClick () {
  fileRef.value?.input.click()
}

async function onSubmit (event: FormSubmitEvent<any>) {
  // Do something with data
  console.log(event.data)

  toast.add({ title: 'Profile updated', icon: 'i-heroicons-check-circle' })
}
</script>

<template>
  <UDashboardPanelContent class="pb-24 pl-40 pr-40">
    <UDivider class="mb-4" />
    <UForm :state="state" :validate="validate" :validate-on="['submit']" @submit="onSubmit">
      <UDashboardSection title="生成项目" description="请务必填写完整信息，以确保项目生成成功。">

        <UFormGroup
          name="name"
          label="项目名称"
          description="例如: TabooGenerate"
          required
          class="grid grid-cols-2 gap-2 items-center"
          :ui="{ container: '' }"
        >
          <UInput v-model="state.name" autocomplete="off" icon="i-heroicons-user" size="md" />
        </UFormGroup>

        <UFormGroup
          name="package"
          label="包路径"
          description="例如: com.github.taboo.generate"
          required
          class="grid grid-cols-2 gap-2"
          :ui="{ container: '' }"
        >
          <UInput v-model="state.package" type="email" autocomplete="off" icon="i-heroicons-envelope" size="md" />
        </UFormGroup>
      </UDashboardSection>
    </UForm>

    <UDivider class="mb-4" />

    <UDashboardSection title="Account" description="No longer want to use our service? You can delete your account here. This action is not reversible. All information related to this account will be deleted permanently.">
      <div>
        <UButton color="red" label="Delete account" size="md" @click="isDeleteAccountModalOpen = true" />
      </div>
    </UDashboardSection>
  </UDashboardPanelContent>
</template>
