<script setup lang="ts">
import { useHead } from '@unhead/vue';
import { computed } from 'vue';
import { useI18n } from 'vue-i18n';
import { useRoute } from 'vue-router';
import RequestForm from './request.vue';
import ResetForm from './reset.vue';

const { t } = useI18n();

const route = useRoute();

const resetToken = computed(() => (Array.isArray(route.query.token) ? route.query.token[0] : route.query.token));

useHead({
	title: t('reset_password'),
});
</script>

<template>
	<public-view>
		<h1 class="type-title">{{ t('reset_password') }}</h1>

		<request-form v-if="!resetToken" />
		<reset-form v-else :token="resetToken" />

		<template #notice>
			<v-icon name="lock" left />
			{{ t('not_authenticated') }}
		</template>
	</public-view>
</template>

<style lang="scss" scoped>
h1 {
	margin-block-end: 20px;
}
</style>
