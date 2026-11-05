<script setup lang="ts">
import { defineBlock } from '@bagelink/blox'
import { Btn, Icon, defineSchema, $ } from '@bagelink/vue'

interface Step { title?: string; text?: string; icon?: string }
interface Props { kicker?: string; heading?: string; intro?: string; steps?: Step[]; cta_label?: string; cta_href?: string }

const schema = defineSchema<Props>({
	kicker: $.text('Kicker'),
	heading: $.text('Heading'),
	intro: $.textarea('Intro'),
	steps: $.array('Steps', defineSchema({
		title: $.text('Title'),
		text: $.textarea('Text'),
		icon: $.text('Icon'),
	}), { collapsible: true, allowReorder: true }),
	cta_label: $.text('Button'),
	cta_href: $.text('Button link'),
})

defineBlock({
	name: 'Steps',
	label: 'Steps',
	icon: 'format_list_numbered',
	category: 'content',
	order: 30,
	description: 'Numbered steps with icons and an optional action.',
	schema,
	defaults: { steps: [] },
})

const props = withDefaults(defineProps<Props>(), { steps: () => [] })
</script>

<template>
	<section class="px-2 m_px-1 py-4">
		<div class="w-1100px mx-auto">
			<p v-if="props.kicker" class="txt12 uppercase tracking-wider quiet m-0 mb-1">{{ props.kicker }}</p>
			<h2 class="txt-32 line-height-12 m-0">{{ props.heading }}</h2>
			<p v-if="props.intro" class="line-height-15 measure m-0 mt-1">{{ props.intro }}</p>
			<ol class="bare grid grid-wrap-4 m_grid-wrap-1 gap-2 mt-3">
				<li v-for="(step, i) in props.steps" :key="step.title || i" class="border-top pt-1">
					<div class="flex space-between align-items-center">
						<span class="txt12 quiet">{{ String(i + 1).padStart(2, '0') }}</span>
						<Icon v-if="step.icon" :name="step.icon" />
					</div>
					<h3 class="txt-20 m-0 mt-05">{{ step.title }}</h3>
					<p class="line-height-15 quiet m-0 mt-05">{{ step.text }}</p>
				</li>
			</ol>
			<Btn v-if="props.cta_label" class="mt-2" outline icon-end="arrow_forward" :value="props.cta_label" :href="props.cta_href || '/contact'" />
		</div>
	</section>
</template>
