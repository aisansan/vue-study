<template>
	<div>
		modal
		<a-modal v-model="visible" ref="modal" title="Basic Modal" @ok="handleOk">
			<Form @update="update" :current_data="current_data"></Form>
		</a-modal>
	</div>
</template>
<script>
	import Form from "@/views/form"
	export default {
		components: {
			Form
		},
		props:{
			current_data:{
				type:Object,
				default:null
				
			}
		},
		data() {
			return {
				visible: false
			};
		},
		methods: {
			showModal() {
				this.visible = true;
			},
			handleOk(e) {
				console.log(e);
				this.visible = false;
			},
			update(e){
				console.log("modal")
				console.log(e)
				this.$emit('updateData',e)
			}
		},
	};
</script>
