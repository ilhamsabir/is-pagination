# Is Pagination

This is vue component for pagination navigation.
[Live Demo Here](https://codesandbox.io/s/demo-is-pagination-xdjcc).


### Installation
```sh
$ npm install is-pagination
```

### Setup
##### Global
```javascript
import IsPagination from 'is-pagination';

Vue.use(IsPagination)

```

### Usage
```html
<template>
  <div id="app">
    <Is-Pagination
		:is-loading="isLoading"
		:pagination-pages="allPages"
		:last-page="lastPage"
		:current-page="currentPage"
		@page-change="pageChange"
	/>
  </div>
</template>

<script>
import IsPagination from 'is-pagination'

export default {
  name: 'App',
  components: {
    IsPagination
	},
	data() {
		return {
			isLoading: false,
			currentPage: 1,
			lastPage: 40,
		}
	},
	computed: {
		allPages() {
			const arr = Array.from(Array(102).keys());
			return arr.length;
		},
	},
	methods: {
		pageChange(value) {
			this.currentPage = value;
			// do something here
		},
	}
}
</script>

<style lang="scss">
.pagination {
  display: flex;
	list-style: none;
	border-radius: .25rem;
}

.page-link {
	position: relative;
	display: block;
	padding: .5rem .75rem;
	margin-left: -1px;
	line-height: 1.25;
	color: #007bff;
	background-color: #fff;
	border: 1px solid #dee2e6;
	text-decoration: none;


  &:hover {
		z-index: 2;
		color: #0056b3;
		text-decoration: none;
		background-color: #e9ecef;
		border-color: #dee2e6;
  }

  &:focus {
    z-index: 3;
    outline: 0;
    box-shadow: 0 0 0 0 rgba(0,123,255,.25);
  }
}

.page-item {
  &:first-child {
    .page-link {
      margin-left: 0;
      border-left-radius: .25rem;
    }
  }
  &:last-child {
    .page-link {
      border-right-radius: .25rem;
    }
  }

  &.active .page-link {
		z-index: 3;
		color: #fff;
		background-color: #007bff;
		border-color: #007bff;
  }

  &.disabled .page-link {
		color: #6c757d;
		pointer-events: none;
		cursor: auto;
		background-color: #fff;
		border-color: #dee2e6;
  }
}


//
// Sizing
//
.pagination-lg .page-link {
  padding: 0.75rem 1.5rem;
  font-size: 1.25rem;
  line-height: 1.5;
}

.pagination-lg .page-item:first-child .page-link {
  border-top-left-radius: 0.3rem;
  border-bottom-left-radius: 0.3rem;
}

.pagination-lg .page-item:last-child .page-link {
  border-top-right-radius: 0.3rem;
  border-bottom-right-radius: 0.3rem;
}

.pagination-sm .page-link {
  padding: 0.25rem 0.5rem;
  font-size: 0.875rem;
  line-height: 1.5;
}

.pagination-sm .page-item:first-child .page-link {
  border-top-left-radius: 0.2rem;
  border-bottom-left-radius: 0.2rem;
}

.pagination-sm .page-item:last-child .page-link {
  border-top-right-radius: 0.2rem;
  border-bottom-right-radius: 0.2rem;
}


</style>


```

## Attributes

- __is-loading:__ Set Loading (Boolean), default false.
- __pagination-pages:__ Set total pages (Integer), default 1.
- __current-page:__ Set Current/Active page (Integer), default 1.
- __last-page:__ Set last page (Integer), default 1.

## Events

#### @page-change

Event is fired when emit page change (next/prev page or hit on page number).

## License
MIT license

© 2020 [Ilham Sabir](https://github.com/ilhamsabir)