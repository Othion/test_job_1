<template>
	<article class="user">
		<div class="user__avatar-wrapper">
			<img 
				class="user__avatar"
				:class="{ 
					'-first-place': place === 1,
					'-second-place': place === 2,
					'-third-place': place === 3
				}"
				src="@/assets/icons/user_na.svg" 
				alt="user-avatar" 
			>
		</div>

		<div class="user__info-left">
			<div class="user__name">
				{{fullName}}
			</div>

			<div class="user__position">
				Position
			</div>
		</div>

		<div class="user__info-right">
			<div class="user__rating-value">
				{{userInfo.rating}}
			</div>

			<div class="user__rating-label">
				{{pluralize(userInfo.rating, ['балл', 'балла', 'баллов'])}}
			</div>
		</div>
	</article>
</template>

<script>
import { pluralize } from '@/utils/helpers'

export default {
	props: {
		userInfo: {
			type: Object,
			default: () => ({
				name: 'user-name',
				secondName: 'user-second-name',
				age: 20,
				rating: 100
			})
		},
		place: {
			type: Number,
			default: 0
		}
	},
	computed: {
		fullName() {
			return `${this.userInfo.name} ${this.userInfo.secondName}`
		}
	},
	methods: {
		pluralize
	}
}
</script>

<style lang="scss" scoped>
.user {
	width: 300px;
	display: flex;
	align-items: center;
	padding: 10px;
	flex-grow: 1;

	&__avatar {
		width: 60px;
		height: 60px;
		border-radius: 50%;
		pointer-events: none;

		&-wrapper {
			width: 100px;
			margin-right: 15px;
		}

		&.-first-place {
			width: 90px;
			height: 90px;
			background: #ffd700;
		}

		&.-second-place {
			width: 80px;
			height: 80px;
			background: #c0c0c0;
		}

		&.-third-place {
			width: 70px;
			height: 70px;
			background: #cd7f32;
		}
	}

	&__info-left,
	&__info-right {
		display: flex;
		flex-direction: column;
	}

	&__info-left {
		margin-right: auto;
		align-items: flex-start;
	}

	&__info-right {
		align-items: flex-end;
	}

	&__name,
	&__rating-value {
		font-weight: bold;
		margin-bottom: 5px;
	}

	&__position,
	&__rating-label {
		font-size: 12px;
		color: gray;
		font-weight: bold;
	}

}
</style>