<template>
	<!-- pagination -->
	<div
		v-if="paginationPages > 1"
		class="block-footer mt-5 float-right">
		<nav
			v-if="!isLoading"
			aria-label="Page navigation example">
			<ul class="pagination">
				<li
					v-if="currentPage > 1"
					class="page-item">
					<a
						class="page-link"
						href="#"
						aria-label="Previous"
						@click.stop.prevent="pageChange(currentPage - 1)">
						<span aria-hidden="true">&laquo;</span>
						<!-- <span class="sr-only">Previous</span> -->
					</a>
				</li>
				<li
					v-for="(item, index) in visiblePaginationPages"
					:key="index"
					:class="{'active' : currentPage === item }"
					class="page-item">
					<span
						v-if="item === '...'"
						class="page-link">
						{{ item }}
					</span>
					<a
						v-else
						class="page-link"
						href="#"
						@click.stop.prevent="pageChange(item)">
						{{ item }}
					</a>
				</li>
				<li
					v-if="currentPage < parseInt(lastPage)"
					class="page-item">
					<a
						class="page-link"
						href="#"
						aria-label="Next"
						@click.stop.prevent="pageChange(currentPage + 1)">
						<span aria-hidden="true">&raquo;</span>
						<!-- <span class="sr-only">Next</span> -->
					</a>
				</li>
			</ul>
		</nav>
	</div>
</template>

<script>
// import { formatNumberPlain } from '../../lib/utils/helper'

export default {
	name: 'IsPagination',
	props: {
		paginationPages: {
			type: Number,
			default: 0,
		},
		currentPage: {
			type: Number,
			default: 1,
		},
		lastPage: {
			type: Number,
			default: 1,
		},
		isLoading: {
			type: Boolean,
			default: false,
		},
	},
	computed: {
		visiblePaginationPages() {
			const pages = []
			const paginationLength = 7
			const pageStep = 3
			let minPage = this.currentPage - pageStep

			if (minPage < 1) minPage = 1
			let maxPage = this.currentPage + pageStep
			if (maxPage < paginationLength) {
				maxPage = new Number(paginationLength)
			}

			if (maxPage > this.paginationPages) {
				maxPage = new Number(this.paginationPages)
			}
			for (let index = minPage; index <= maxPage; index++) {
				pages.push(index)
			}
			if (maxPage > paginationLength) {
				pages.unshift('...')
				pages.unshift(1)
			}
			if (this.currentPage < (this.paginationPages - paginationLength)) {
				pages.push('...')
				pages.push(this.paginationPages)
			}
			return pages
		},
	},
	methods: {
		// page change
		pageChange(val) {
			window.scrollTo(0, 0)
			this.$emit('page-change', val)
		},
	},
}
</script>
