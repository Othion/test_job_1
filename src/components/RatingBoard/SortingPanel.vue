<template>
	<article class="sorting-panel">
		<button
			type="button" 
			class="sorting-panel__age-sort"
			:class="{ '-active': sortField === SortFieldsEnum.age && isSortingActive }"
			@click="sort(SortFieldsEnum.age)"
		>
			<div class="sorting-panel__label">
				Возраст
			</div>

			<span 
				class="sorting-panel__icon"
				:class="{ 
					'-desc': sortField === SortFieldsEnum.age 
						&& sortType === SortTypesEnum.DESC 
				}"
			>
				⬆
			</span>
		</button>

		<button 
			type="button"
			class="sorting-panel__rating-sort"
			:class="{ '-active': sortField === SortFieldsEnum.rating && isSortingActive }"
			@click="sort(SortFieldsEnum.rating)"
		>
			<div class="sorting-panel__label">
				Рейтинг
			</div>

			<span 
				class="sorting-panel__icon"
				:class="{ 
					'-desc': sortField === SortFieldsEnum.rating 
						&& sortType === SortTypesEnum.DESC  
				}"
			>
				⬆
			</span>
		</button>

	</article>
</template>

<script>
import { SortFieldsEnum, SortTypesEnum } from '@/utils/Enums'

export default {
	props: {
		sortField: {
			type: Number,
		},
		sortType: {
			type: Number
		}
	},
	data() {
		return {
			SortFieldsEnum,
			SortTypesEnum
		}
	},
	computed: {
		isSortingActive() {
			return this.sortType !== this.SortTypesEnum.noSorting
		}
	},
	methods: {
		sort(field) {
			if (field === this.sortField) {
				if (this.sortType === this.SortTypesEnum.ASC) {
					this.$emit('sort', { sortField: field, sortType: SortTypesEnum.noSorting})
				} else {
					this.$emit('sort', { sortField: field, sortType: this.sortType + 1})
				}
			} else {
				this.$emit('sort', { sortField: field, sortType: SortTypesEnum.DESC})
			}
		}
	}
}
</script>

<style lang="scss" scoped>
.sorting-panel {
	display: flex;
	align-items: center;
	justify-content: center;
	margin-bottom: 25px;

	&__age-sort,
	&__rating-sort {
		background: none;
		border: none;
		outline: none;
		cursor: pointer;
		display: flex;
		transition: color 160ms ease;

		&.-active {
			color: #2c95f1;
		}
	}

	&__icon {
		&.-desc {
			transform: rotate(180deg);
		}
	}

	&__label {
		margin-right: 5px;
	}

	&__age-sort {
		margin-right: 15px;
	}
}
</style>