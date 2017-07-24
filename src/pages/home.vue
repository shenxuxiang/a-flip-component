<template>
    <div class="home-page">
        <page-component
        	:maxPage="2"
        	@emitQequestPage="requestPage"
        ></page-component>
    </div>
</template>

<script>
import PageComponent from '../components/pagecomponent.vue'
    export default {
    	components: { PageComponent },
    	data () {
    		return {

    		}
    	},
    	methods: {
    		requestPage (num) { // 请求翻页功能 这里发送ajax
    			console.log('请求翻页功能 这里可以发送ajax请求：第' + num + '页')
    		}
    	}
    }
</script>

<style scoped lang="scss">

</style>