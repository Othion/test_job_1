<template>
	<section class="rating-board">
		<header class="rating-board__heading">
			<h1 class="rating-board__heading-label">
				Рейтинг участников
			</h1>

			<search-panel 
				@search="searchUser"
			/>

		</header>

		<sorting-panel 
			:sort-field="sortField"
			:sort-type="sortType"
			@sort="sortUsers"
		/>

		<user-list 
			:user-list="sortedUsers"
		/>

		<footer v-if="searchedUser !== null" class="rating-board__footer">
			<div class="rating-board__place-wrapper">
				<div class="rating-board__current-place">
					{{currentUserPlace}}
				</div>

				<div class="rating-board__users-count">
					из {{users.length}}
				</div>
			</div>
			<User :user-info="searchedUser"/>
		</footer>

		<footer v-if="userNotFound" class="rating-board__footer">
			<div class="rating-board__user-not-found">
				Пользователь не найден
			</div>
		</footer>

	</section>
</template>

<script>
import UserList from './UserList'
import User from './User'
import SearchPanel from './SearchPanel'
import SortingPanel from './SortingPanel'
import { SortFieldsEnum, SortTypesEnum } from '@/utils/Enums'

import { users } from '@/assets/users'

export default {
	components: {
		UserList,
		SearchPanel,
		User,
		SortingPanel
	},
	data() {
		return {
			searchedUser: null,
			userNotFound: false,
			currentUserPlace: 0,
			sortField: 0,
			sortType: SortTypesEnum.noSorting,
			users
		}
	},
	computed: {
		sortedUsers() {
			if (this.sortType === SortTypesEnum.noSorting) {
				return this.users
			} else {
				if (this.sortField === SortFieldsEnum.age) {
					if (this.sortType === SortTypesEnum.ASC) {
						return [...users].sort((firstVal, secondVal) => {
							return firstVal.age - secondVal.age
						})
					} else {
						return [...users].sort((firstVal, secondVal) => {
							return secondVal.age - firstVal.age
						})
					}
				} else {
					if (this.sortType === SortTypesEnum.ASC) {
						return [...users].sort((firstVal, secondVal) => {
							return firstVal.rating - secondVal.rating
						})
					} else {
						return [...users].sort((firstVal, secondVal) => {
							return secondVal.rating - firstVal.rating
						})
					}
				}
			}
		}
	},
	methods: {
		searchUser(e) {
			this.searchedUser = null
			this.userNotFound = false

			this.sortedUsers.forEach((user, index) => {
				let userFullName = `${user.name} ${user.secondName}`

				if (userFullName === e.trim()) {
					this.searchedUser = user
					this.currentUserPlace = index + 1
					
					return
				}
			})

			if (this.searchedUser === null) {
				this.userNotFound = true

				setTimeout(() => {
					this.userNotFound = false
				}, 5000)
			} else {
				return
			}
		},
		sortUsers(e) {
			this.sortField = e.sortField
			this.sortType = e.sortType
		}
	}
}
</script>

<style lang="scss" scoped>
.rating-board {
	display: flex;
	flex-direction: column;
	height: 100%;

	&__heading {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 20px;
		margin-top: 20px;

		&-label {
			font-size: 20px;
			margin: 0;
		}
	}

	&__footer {
		display: flex;
		align-items: center;
		padding: 10px 100px 10px 40px;
		border-top: 1px solid lightgray;
	}

	&__place-wrapper {
		width: 50px;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		font-size: 13px;
	}

	&__users-count {
		color: gray;
		font-weight: bold;
	}

	&__user-not-found {
		display: flex;
		justify-content: center;
		flex-grow: 1;
		padding: 20px 0;
		font-size: 16px;
		color: gray;
	}
}
</style>