<script setup lang="ts">
import { defineBlock } from '@bagelink/blox'
import { Btn, defineSchema, $ } from '@bagelink/vue'

interface Props {
	kicker?: string
	title?: string
	body?: string
	cta_label?: string
	cta_href?: string
	cta2_label?: string
	cta2_href?: string
	image?: string
	image_alt?: string
	caption?: string
}

const schema = defineSchema<Props>({
	kicker: $.text('Kicker'),
	title: $.text('Titre'),
	body: $.textarea('Texte'),
	cta_label: $.text('Bouton'),
	cta_href: $.text('Lien du bouton'),
	cta2_label: $.text('Bouton secondaire'),
	cta2_href: $.text('Lien secondaire'),
	image: $.text('Image'),
	image_alt: $.text('Texte alt'),
	caption: $.text('Légende'),
})

defineBlock({
	name: 'Hero',
	label: 'Hero',
	icon: 'landscape',
	category: 'hero',
	order: 10,
	description: 'Ouverture éditoriale : un titre serif, deux actions, une grande image.',
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
				<h1 class="display m-0">{{ props.title }}</h1>
				<p v-if="props.body" class="txt-18 line-height-15 measure m-0 mt-1">{{ props.body }}</p>
				<div class="flex gap-1 flex-wrap mt-2">
					<Btn v-if="props.cta_label" size="lg" icon-end="arrow_forward" :value="props.cta_label" :href="props.cta_href || '/contact'" />
					<Btn v-if="props.cta2_label" size="lg" outline :value="props.cta2_label" :href="props.cta2_href || '/journal'" />
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
