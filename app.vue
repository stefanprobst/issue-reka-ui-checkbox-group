<script setup lang="ts">
import { Checkbox } from "reka-ui/namespaced";
import { CheckIcon } from "lucide-vue-next";

function onSubmit(event: Event) {
	const form = event.currentTarget as HTMLFormElement;
	const formData = new FormData(form);
	const fruits = formData.getAll("Fruits");
	alert(JSON.stringify({ fruits }));

	/**
	 * Form data actually is:
	 * ```json
	 * {
   * 	"[fruits][0]": "orange",
   * 	"[fruits][1]": "banana"
	 *	}
	 * ```
	 */
	console.log(Object.fromEntries(formData.entries()))
}

const items = [
	{ value: "apple", label: "Apple" },
	{ value: "banana", label: "Banana" },
	{ value: "kiwi", label: "Kiwi" },
	{ value: "orange", label: "Orange" },
];
</script>

<template>
	<form class="p-8 grid gap-y-8" @change="onSubmit" @submit.prevent="onSubmit">
		<Checkbox.GroupRoot name="fruits" class="grid gap-y-3">
			<label v-for="item in items" :key="item.value" class="flex gap-x-2 items-center">
				<Checkbox.Root :value="item.value" class="size-5 rounded-md shadow border border-neutral-300">
					<Checkbox.Indicator
						class="bg-white size-full grid place-content-center"
					>
						<CheckIcon class="size-4" />
					</Checkbox.Indicator>
				</Checkbox.Root>
				<span class="select-none">{{ item.label }}</span>
			</label>
		</Checkbox.GroupRoot>

		<div>
			<button class="px-4 py-2 rounded-md bg-green-600 text-sm font-medium text-white" type="submit">Submit</button>
		</div>
	</form>
</template>
