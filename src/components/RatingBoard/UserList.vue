<template>
	<transition-group name="flip-list" tag="ul" class="user-list">
		<li 
			class="user-list__user-wrapper"
			v-for="(user, index) in userList"
			:key="user.id"
		>
			<span class="user-list__user-place">
				{{index + 1}}
			</span>
			<user 
				:user-info="user"
				:place="index + 1"
			/>
		</li>
	</transition-group>
</template>

<script>
import User from './User.vue'

export default {
	components: {
		User
	},
	props: {
		userList: {
			type: Array,
			default: () => []
		}
	}	
}
</script>

<style lang="scss" scoped>

.flip-list-move {
  transition: transform 1.5s;
}

.user-list {
	margin: 0;
	padding: 0;
	list-style: none;
	display: flex;
	flex-direction: column;
	padding: 0 100px 0 40px;
	overflow: auto;

	&__user {

		&-wrapper {
			display: flex;
			align-items: center;
		}

		&-place {
			width: 50px;
			font-size: 13px;
			text-align: left;
		}
	}
}
</style>