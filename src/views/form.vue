<template>
  <a-form :form="form" :label-col="{ span: 5 }" :wrapper-col="{ span: 12 }" @submit="handleSubmit">
	  <a-form-item label="key">
	    <a-input
	      v-decorator="['key', {initialValue:current_data.key, rules: [{ required: true, message: 'Please input your key!' }] }]"
	    />
	  
	  </a-form-item>
    <a-form-item label="name">
      <a-input
        v-decorator="['name', {initialValue:current_data.name, rules: [{ required: true, message: 'Please input your name!' }] }]"
      />

    </a-form-item>
    <a-form-item label="age">
      <a-input
        v-decorator="['age', {initialValue:current_data.age, rules: [{ required: true, message: 'Please input your age!' }] }]"
      />

    </a-form-item>
    <a-form-item label="address">
      <a-input
        v-decorator="['address', {initialValue:current_data.address, rules: [{ required: true, message: 'Please input your adress!' }] }]"
      />

    </a-form-item>
    <a-form-item label="tags">
      <a-input
        v-decorator="['tags', {initialValue:this.tags, rules: [{ required: true, message: 'Please input your tags!' }] }]"
      />

    </a-form-item>

    <a-form-item :wrapper-col="{ span: 12, offset: 5 }">
      <a-button type="primary" html-type="submit">
        更新
      </a-button>
    </a-form-item>
<!--    {{test_data}}-->
<!--    {{current_data_form?current_data_form.age:123}}-->
  </a-form>
</template>

<script>
  export default {
    data() {
      return {
        formLayout: 'horizontal',
        form: this.$form.createForm(this, { name: 'coordinated' }),
      };
    },
	computed:{
		tags(){
			return this.current_data.tags.join(',')
		}
	},
	props:{
		current_data:{
			type:Object,
			default:{
				name:"",
				age:"",
				tags:[],
				address:""
			}
		}
	},
    methods: {
      handleSubmit(e) {
        e.preventDefault();
        this.form.validateFields((err, values) => {
          if (!err) {
            console.log('Received values of form: ', values);
				this.$emit('update',values)
				this.form.resetFields()
          }
        });
	
	
		
      }
      // handleSelectChange(value) {
      //   console.log(value);
      //   this.form.setFieldsValue({
      //     note: `Hi, ${value === 'male' ? 'man' : 'lady'}!`,
      //   });
      // },
    },
  };
</script>