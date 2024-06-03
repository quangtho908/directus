<script setup lang="ts">
import { computed } from 'vue';
import { useI18n } from 'vue-i18n';

type Link = {
	icon: string;
	name: string;
	to?: string;
	href?: string;
	chip?: string;
};

const { t } = useI18n();

const links = computed<Link[][]>(() => [
	[
		{
			icon: 'database',
			name: t('settings_data_model'),
			to: `/settings/data-model`,
		},
		{
			icon: 'admin_panel_settings',
			name: t('settings_permissions'),
			to: `/settings/roles`,
		},
		{
			icon: 'bolt',
			name: t('settings_flows'),
			to: `/settings/flows`,
		},
	],
	[
		{
			icon: 'tune',
			name: t('settings_project'),
			to: `/settings/project`,
		},
		{
			icon: 'palette',
			name: t('settings_appearance'),
			to: `/settings/appearance`,
		},
		{
			icon: 'bookmark',
			name: t('settings_presets'),
			to: `/settings/presets`,
		},
		{
			icon: 'translate',
			name: t('settings_translations'),
			to: `/settings/translations`,
		},
	],
	[
		{
			icon: 'category',
			name: t('extensions'),
			to: '/settings/extensions',
		},
	]
]);
</script>

<template>
	<v-list nav>
		<template v-for="(group, index) in links">
			<v-list-item v-for="item in group" :key="item.to ?? item.href" :to="item.to" :href="item.href">
				<v-list-item-icon><v-icon :name="item.icon" /></v-list-item-icon>
				<v-list-item-content>
					<span class="label">
						<v-text-overflow class="label" :text="item.name" />
						<v-chip v-if="item.chip" class="chip" outlined x-small>{{ item.chip }}</v-chip>
					</span>
				</v-list-item-content>
			</v-list-item>

			<v-divider v-if="index !== links.length - 1" :key="index" />
		</template>

	</v-list>
</template>

<style scoped>
.version .v-icon {
	color: var(--theme--foreground-subdued);
	transition: color var(--fast) var(--transition);
}

.version :deep(.v-text-overflow) {
	color: var(--theme--foreground-subdued);
	transition: color var(--fast) var(--transition);
}

.version:hover .v-icon {
	color: var(--theme--foreground-accent);
}

.version:hover :deep(.v-text-overflow) {
	color: var(--theme--foreground-accent);
}

.label {
	display: flex;
	align-items: center;
}

.chip {
	--v-chip-color: var(--theme--primary);
	--v-chip-background-color: var(--theme--primary-subdued);
	margin-inline-start: auto;
}
</style>
