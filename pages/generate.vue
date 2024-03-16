<script setup lang="ts">
import type { FormError, FormSubmitEvent } from '#ui/types'

const state = reactive({
  name: 'TabooGenerate',
  package: 'com.github.taboo.generate',
})

const toast = useToast()

function validate (state: any): FormError[] {
  const errors = []
  if (!state.name) errors.push({ path: 'name', message: 'Please enter your name.' })
  if (!state.email) errors.push({ path: 'email', message: 'Please enter your email.' })
  if ((state.password_current && !state.password_new) || (!state.password_current && state.password_new)) errors.push({ path: 'password', message: 'Please enter a valid password.' })
  return errors
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
          <UInput v-model="state.name" autocomplete="off" size="md" />
        </UFormGroup>

        <UFormGroup
          name="package"
          label="包路径"
          description="例如: com.github.taboo.generate"
          required
          class="grid grid-cols-2 gap-2"
          :ui="{ container: '' }"
        >
          <UInput v-model="state.package" type="email" autocomplete="off" size="md" />
        </UFormGroup>
        <UFormGroup
          name="module"
          label="模块"
          description=""
          required
          class="grid grid-cols-2 gap-2"
          :ui="{ container: '' }"
        >
          <UCheckbox label="UNIVERSAL" help="聚合模块, 已包含: CHAT, CONFIGURATION, LANG, EXPANSION_COMMAND_HELPER" :model-value="true" />
          <UCheckbox label="BUKKIT_ALL" help="聚合模块, 已包含: BUKKIT, BUKKIT_HOOK, BUKKIT_UTIL, BUKKIT_XSERIES" :model-value="true" />
          <UCheckbox label="AI" help="管理与注册自定义实体 AI（Pathfinder）。" :model-value="false" />
          <UCheckbox label="BUKKIT_HOOK" help="Bukkit 第三方插件支持，例如 Placeholder, Vault 等。" :model-value="false" />
          <UCheckbox label="BUKKIT_UTIL" help="Bukkit 拓展工具。" :model-value="false" />
          <UCheckbox label="BUKKIT_XSERIES" help="Bukkit XSeries 支持。" :model-value="false" />
          <UCheckbox label="CHAT" help="Raw 信息构建工具与 1.16 RGB 颜色转换。" :model-value="false" />
          <UCheckbox label="CONFIGURATION" help="配置文件解决方案（Yaml & Toml & Hocon & Json)" :model-value="false" />
          <UCheckbox label="DATABASE" help="基于 HikariCP 的数据库管理工具（SQL & SQLite）。" :model-value="false" />
          <UCheckbox label="EFFECT" help="莫式粒子库。" :model-value="false" />
          <UCheckbox label="KETHER" help="内建脚本（动作语句）解决方案。" :model-value="false" />
          <UCheckbox label="LANG" help="语言文件解决方案。" :model-value="false" />
          <UCheckbox label="METRICS" help="bStats 整合。" :model-value="false" />
          <UCheckbox label="NAVIGATION" help="无实体寻路工具。" :model-value="false" />
          <UCheckbox label="NMS" help="跨版本 nms 解决方案与数据包管理工具。" :model-value="false" />
          <UCheckbox label="NMS_UTIL" help="常用 nms 工具集合。" :model-value="false" />
          <UCheckbox label="PORTICUS" help="BungeeCord 通讯工具。" :model-value="false" />
          <UCheckbox label="UI" help="箱子菜单构建工具。" :model-value="false" />
        </UFormGroup>
        <UFormGroup
          name="expand"
          label="拓展模块"
          description=""
          required
          class="grid grid-cols-2 gap-2"
          :ui="{ container: '' }"
        >
          <UCheckbox label="EXPANSION_REDIS" help="Redis 操作工具。" :model-value="false" />
          <UCheckbox label="EXPANSION_COMMAND_HELPER" help="命令帮助扩展模块。" :model-value="false" />
          <UCheckbox label="EXPANSION_JAVASCRIPT" help="JavaScript 扩展模块。" :model-value="false" />
          <UCheckbox label="EXPANSION_PTC" help="持久化容器扩展模块。" :model-value="false" />
          <UCheckbox label="EXPANSION_PTC_OBJECT" help="持久化容器扩展模块。" :model-value="false" />
          <UCheckbox label="EXPANSION_PLAYER_DATABASE" help="玩家持久化数据扩展模块。" :model-value="false" />
          <UCheckbox label="EXPANSION_PLAYER_FAKE_OP" help="玩家伪 OP 权限扩展模块。" :model-value="false" />
          <UCheckbox label="EXPANSION_SUBMIT_CHAIN" help="对 Coroutine API 的封装扩展模块。" :model-value="false" />
        </UFormGroup>
        <UFormGroup
          name="platform"
          label="平台"
          description=""
          required
          class="grid grid-cols-2 gap-2"
          :ui="{ container: '' }"
        >
          <UCheckbox label="BUKKIT" help="Bukkit系列运行环境" :model-value="false" />
          <UCheckbox label="BUNGEE" help="Bungee系列运行环境" :model-value="false" />
          <UCheckbox label="VELOCITY" help="Velocity系列运行环境" :model-value="false" />
        </UFormGroup>
      </UDashboardSection>
    </UForm>

    <UDivider class="mb-4" />

    <UDashboardSection title="鸣谢名单" description="坏黑、自由、大阔吖、ShellWen⚝ | 颉文">
      <div>
        <UButton label="生成项目" size="md" />
      </div>
    </UDashboardSection>
  </UDashboardPanelContent>
</template>
