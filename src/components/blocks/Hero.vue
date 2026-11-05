<script setup lang="ts">
import { defineBlock } from '@bagelink/blox'
import { Btn, defineSchema, $ } from '@bagelink/vue'

interface Props {
	kicker?: string
	heading?: string
	subheading?: string
	primary_label?: string
	primary_href?: string
	secondary_label?: string
	secondary_href?: string
	image?: string
	image_alt?: string
	caption?: string
}

const schema = defineSchema<Props>({
	kicker: $.text('Kicker'),
	heading: $.text('Heading'),
	subheading: $.textarea('Subheading'),
	primary_label: $.text('Primary label'),
	primary_href: $.text('Primary link'),
	secondary_label: $.text('Secondary label'),
	secondary_href: $.text('Secondary link'),
	image: $.text('Image'),
	image_alt: $.text('Image alt'),
	caption: $.text('Caption'),
})

defineBlock({
	name: 'Hero',
	label: 'Hero',
	icon: 'landscape',
	category: 'hero',
	order: 10,
	description: 'Editorial hero with a serif headline, two actions and a large image.',
	schema,
	defaults: {},
})

const props = defineProps<Props>()
</script>

<template>
	<section class="px-2 m_px-1">
		<div class="w-1100px mx-auto grid grid-2-col m_grid-wrap-1 gap-3 align-items-center stone">
			<div class="pb-4">
				<p v-if="props.kicker" class="txt12 uppercase tracking-wider quiet m-0 mb-1">{{ props.kicker }}</p>
				<h1 class="display m-0">{{ props.heading }}</h1>
				<p v-if="props.subheading" class="txt-18 line-height-15 measure m-0 mt-1">{{ props.subheading }}</p>
				<div class="flex gap-1 flex-wrap mt-2">
					<Btn v-if="props.primary_label" size="lg" icon-end="arrow_forward" :value="props.primary_label" :href="props.primary_href || '/contact'" />
					<Btn v-if="props.secondary_label" size="lg" outline :value="props.secondary_label" :href="props.secondary_href || '/journal'" />
				</div>
			</div>
			<figure v-if="props.image" class="m-0">
				<div class="frame hero-frame">
					<img :src="props.image" :alt="props.image_alt || ''" />
				</div>
				<figcaption v-if="props.caption" class="txt14 quiet mt-075">{{ props.caption }}</figcaption>
			</figure>
		</div>
	</section>
</template>
