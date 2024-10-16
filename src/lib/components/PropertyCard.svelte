<script lang="ts">
	import type { FunctionReturnType } from 'convex/server';
	import { api } from '../../convex/_generated/api';
	import IconBed from './../../../static/icon-bed.svg?component';
	import IconBathroom from './../../../static/icon-bathroom.svg?component';
	import IconBathtub from './../../../static/icon-bathtub.svg?component';
	import IconParking from './../../../static/icon-parking.svg?component';
	// import IconSize from './../../../static/icon-size.svg?component';

	type PropertiesType = FunctionReturnType<typeof api.getProperties.get>;
	type PropertyType = PropertiesType[number];

	let { status, property }: { status: 'for-sale' | 'for-rent'; property: PropertyType } = $props();
</script>

<a href="/properties/{status}/{property.slug}">
	<div
		class="rounded-3xl flex flex-col w-full h-full overflow-hidden shadow-sm transform transition-all duration-300 hover:scale-105 border-2 border-gray-100 hover:border-none hover:shadow-[0_0_0_4px_white] hover:outline hover:outline-2 hover:outline-offset-4 hover:outline-black"
	>
		<!-- TODO: Implement lazy-loading and blurhash -->
		<!-- port to deno https://github.com/npdtdev/blurhash-svelte/tree/master/src/lib/components -->
		<div class="bg-cover bg-center h-full w-[500px] max-w-[900px] max-h-[300px]">
			<img
				data-src={property.assets.images.find((img) => img.is_primary)?.asset_url}
				alt="main"
				class="rounded-t-3xl h-full w-full object-cover"
			/>
		</div>

		<div class="p-4 flex flex-col gap-2">
			<h2 class="font-semibold text-lg">{property.property_title}</h2>
			<h2 class="tracking-wide">
				{property.price.toLocaleString('th-TH', { style: 'currency', currency: 'THB' })}
			</h2>
			<div class="flex gap-5">
				<div class="flex items-center justify-center gap-1">
					<IconBed width="20" />
					{property.bedrooms}
				</div>
				<div class="flex items-center justify-center gap-1">
					<IconBathtub width="20" />
					{property.bathrooms}
				</div>
				<div class="flex items-center justify-center gap-1">
					<IconParking width="20" />
					{property.parking_spots}
				</div>
				<div class="flex items-center justify-center gap-1">
					<!-- <IconSize width="20" /> -->
					<span>{property.plot_size?.toLocaleString()} m<sup>2</sup></span>
				</div>
			</div>
		</div>
	</div>
</a>
