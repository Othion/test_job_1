<template>
	<article class="search-panel">
		<input 
			class="search-panel__input"
			:class="{ '-error': errorMessage }" 
			type="text"
			placeholder="Пользователь" 
			v-model="searchText"
		/>

		<button 
			type="button" 
			class="search-panel__button"
			@click="searchEmitter"
		>
			<img 
				src="@/assets/icons/search.svg" 
				class="search-panel__button-icon" 
				alt="search-icon"
			>
		</button>

		<div v-if="errorMessage" class="search-panel__error-message">
			{{errorMessage}}
		</div>


	</article>
</template>

<script>
export default {
	props: {
		value: {
			type: String
		}
	},
	data() {
		return {
			searchText: '',
			errorMessage: ''
		}
	},
	watch: {
		searchText() {
			if (this.errorMessage) {
				this.errorMessage = ''
			} else {
				return
			}
		}
	},
	methods: {
		searchEmitter() {
			if (this.searchText) {
				this.$emit('search', this.searchText)
			} else {
				this.errorMessage = 'Введите имя и фамилию'

				setTimeout(() => {
					this.errorMessage = ''
				}, 5000)
			}
		}
	}
}
</script>

<style lang="scss" scoped>
.search-panel {
	display: flex;
	align-items: center;
	position: relative;

	&__input {
		height: 32px;
		margin-right: 20px;
		padding: 5px 10px;
		border: none;
		border-bottom: 1px solid lightgray;
		outline: none;

		&.-error {
			border-color: #f00;

			&::placeholder {
				color: #f00;
			}
		}
	}

	&__button {
		cursor: pointer;
		border: none;
		background: #fff;
		display: flex;
		align-items: center;
		justify-content: center;
		outline: none;
		transition: transform 160ms;

		&:hover {
			transform: scale(1.1)
		}

		&-icon {
			width: 30px;
			height: 30px;
		}
	}

	&__error-message {
		color: #f00;
		font-size: 12px;
		position: absolute;
		bottom: -25px;
		left: 10px;
	}
}
</style>