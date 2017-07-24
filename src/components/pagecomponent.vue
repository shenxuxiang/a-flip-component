<template>
	<ul
		class="page-component"
		:style="{width: getWidth, maxWidth: '354px'}"
	>
		<li
			class="page-component-item"
			@click="prevPage"
		>&lt;</li>
		<template
			v-if="maxPage <= 7"
		>
			<li
				v-for="num in maxPage"
				:key="num"
				:class="num === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="activePage(num)"
			>
				{{ num }}
			</li>
		</template>
		<template
			v-else
		>
			<li
				:class="1 === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="activePage(1)"
			>
				1
			</li>

			<li
				:class="2 === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="setCurentPageToTwo(2, $event)"
			>
				{{ currentPage > 4 ? '...' : 2 }}
			</li>

			<li
				:class="getPrevCurrentPage === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="activePage(getPrevCurrentPage)"
			>
				{{ getPrevCurrentPage }}
			</li>

			<li
				:class="getCurrentPage === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="activePage(getCurrentPage)"
			>
				{{ getCurrentPage }}
			</li>

			<li
				:class="getNextCurrentPage === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="activePage(getNextCurrentPage)"
			>
				{{ getNextCurrentPage }}
			</li>

			<li
				:class="maxPage - 1 === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="setCurentPageTolast(maxPage - 1, $event)"
			>
				{{ maxPage - currentPage <= 3  ?  maxPage - 1 : '...' }}
			</li>

			<li
				:class="maxPage === currentPage ? 'page-component-item active' : 'page-component-item'"
				@click="activePage(maxPage)"
			>
				{{ maxPage }}
			</li>
		</template>
		<li
			class="page-component-item"
			@click="nextPage"
		>&gt;</li>
	</ul>
</template>

<script>
	export default {
		props: {
			maxPage: {
				type: Number,
				default: 1
			},
			emitQequestPage: {
				type: Function
			}
		},
		data () {
			return {
				currentPage: 1
			}
		},
		computed: {
			getWidth () { // 获取宽度
				let width = 88 + this.maxPage * 32 + (this.maxPage - 1) * 7
				return width + 'px'
			},
			getPrevCurrentPage () {
				if (this.currentPage > 3 && this.maxPage - this.currentPage > 3) {
					return this.currentPage - 1
				} else if (this.maxPage - this.currentPage <= 3) {
					return this.maxPage - 4
				} 
				else {
					return 3
				}
			},
			getCurrentPage () {
				if (this.currentPage > 3 && this.maxPage - this.currentPage > 3) {
					return this.currentPage
				} else if (this.maxPage - this.currentPage <= 3) {
					return this.maxPage - 3
				} 
				else {
					return 4
				}
			},
			getNextCurrentPage () {
				if (this.currentPage > 3 && this.maxPage - this.currentPage > 3) {
					return this.currentPage + 1
				} else if (this.maxPage - this.currentPage <= 3) {
					return this.maxPage - 2
				} 
				else {
					return 5
				}
			}
		},
		methods: {
			prevPage () { // 上一页
				if (this.currentPage === 1) {
					return
				}
				this.currentPage = this.currentPage > 1 ? this.currentPage - 1 : 1
				this.$emit('emitQequestPage', this.currentPage)
			},
			nextPage () { // 下一页
				if (this.currentPage === this.maxPage) {
					return
				}
				this.currentPage = this.currentPage >= this.maxPage ? this.maxPage : this.currentPage + 1
				this.$emit('emitQequestPage', this.currentPage)
			},
			activePage (num) { // 点击设置成当前页
				this.currentPage = num
				this.$emit('emitQequestPage', num)
			},
			setCurentPageToTwo (num, event) { // 点击第2个页数框
				if (num === +event.target.innerHTML) {
					this.currentPage = num
					this.$emit('emitQequestPage', num)
				}
			},
			setCurentPageTolast (num, event) { // 点击倒数第2个页数框
				if (num === +event.target.innerHTML) {
					this.currentPage = num
					this.$emit('emitQequestPage', num)
				}
			}
		}
	}
</script>

<style scoped lang="scss">
	.page-component {
		width: 276px;
		height: 32px;
		margin-left: 0;
		margin-right: 0;
		margin: auto;
		list-style: none;
	}
	.page-component-item {
		float: left;
		width: 32px;
		height: 32px;
		text-align: center;
		line-height: 30px;
		border: 1px solid #d9d9d9;
		box-sizing: border-box;
		margin-left: 7px;
		cursor:pointer;
		user-select: none;
	}
	.page-component-item:hover {
		background: #374960;
		color: #fff;
	}
	.page-component-item.active {
		background: #374960;
		color: #fff;
	}
	.page-component-item:first-child {
		margin-left: 0;
	}
	.page-component-item:nth-child(2),
	.page-component-item:last-child {
		margin-left: 12px;
	}
</style>