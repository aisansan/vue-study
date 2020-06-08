<template>
	<div>
		<a-table :columns="columns" :data-source="data2">
			<a slot="name" slot-scope="text">{{ text }}</a>
			<span slot="customTitle">
				<a-icon type="smile-o" />姓名</span>
			<span slot="tags" slot-scope="tags">
				<a-tag v-for="tag in tags" :key="tag" :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'">
					{{ tag.toUpperCase() }}
				</a-tag>
			</span>
			<span slot="action" slot-scope="text, record">
				<a @click="edit(record)">edit</a>
			</span>
		</a-table>
		<Modal @updateData="updateData" :current_data="current_data" ref="modal"></Modal>
	</div>

</template>
<script>
	import Modal from "@/views/modal"
	const columns = [{
			dataIndex: 'name',
			key: 'name',
			slots: {
				title: 'customTitle'
			},
			scopedSlots: {
				customRender: 'name'
			},
		},
		{
			title: '年龄',
			dataIndex: 'age',
			key: 'age',
		},
		{
			title: '地址',
			dataIndex: 'address',
			key: 'address',
		},
		{
			title: '职业',
			key: 'tags',
			dataIndex: 'tags',
			scopedSlots: {
				customRender: 'tags'
			},
		},
		{
			title: '编辑',
			key: 'action',
			scopedSlots: {
				customRender: 'action'
			},
		},
	];

	const data1 = [{
			key: '1',
			name: 'John Brown',
			age: 32,
			address: 'New York No. 1 Lake Park',
			tags: ['nice', 'developer'],
		},
		{
			key: '2',
			name: 'Jim Green',
			age: 42,
			address: 'London No. 1 Lake Park',
			tags: ['loser'],
		},
		{
			key: '3',
			name: 'Joe Black',
			age: 32,
			address: 'Sidney No. 1 Lake Park',
			tags: ['cool', 'teacher'],
		},
	];
	//模拟异步操作
	const getData = new Promise(
		(resolve, reject) => {
			setTimeout(() => {
				resolve(data1)
			}, 2000)

		}
	)
	export default {
		// provide(){
		//   return {
		//     current_data_form:this.current_data,
		//     data_form:this.data,
		//     test_data:123
		//   }
		// },
		components: {
			Modal
		},
		created() {
			//通过异步获取数据
			getData.then((data1) => {
				this.data2 = data1
			})
		},
		data() {
			return {
				data2: null,
				current_data: null,
				columns,
			};
		},
		methods: {
			//提交服务器更新数据
			updateData(e) {
				e.tags = e.tags.split(',')
				console.log(e)
				this.current_data = e
				let key = 0;
				for(let i in this.data2){
					if(this.data2[i].key == e.key){
						key = i
					}
				}
				this.$set(this.data2, key, e)
		
				console.log(this.data2)
				console.log("数据更新了")
				console.log(e)
			},
			//编辑单条数据
			edit(r) {
				console.log(r)
				this.current_data = r
				this.$refs.modal.showModal()
			}
		}
	};
</script>
