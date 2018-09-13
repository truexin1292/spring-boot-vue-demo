<template>
	<el-dialog title="Edit" v-model="dialogFormVisible" :close-on-click-modal="false" :show-close="false">
		<el-form :model="form">
			<el-form-item label="item_id" :label-width="formLabelWidth">
				<el-input :disabled="true" v-model="form.id" auto-complete="off"></el-input>
			</el-form-item>
			<el-form-item label="username" :label-width="formLabelWidth">
				<el-input v-model="form.username" auto-complete="off"></el-input>
			</el-form-item>
			<el-form-item label="email" :label-width="formLabelWidth">
				<el-input v-model="form.email" auto-complete="off"></el-input>
			</el-form-item>
			<el-form-item label="phone" :label-width="formLabelWidth">
				<el-input v-model="form.phone" auto-complete="off"></el-input>
			</el-form-item>
			<el-form-item label="sex" :label-width="formLabelWidth">
				<el-select v-model="form.sex" v-on:visible-change="selectDemo">
					<el-option
						v-for="(item, index) in type_options"
						:key="index"
						:label="item.label"
						:value="item.value">
					</el-option>
				</el-select>
			</el-form-item>
			<el-form-item label="zone" :label-width="formLabelWidth">
				<el-input v-model="form.zone" auto-complete="off"></el-input>
			</el-form-item>
		</el-form>
		<div slot="footer" class="dialog-footer">
			<el-button :plain="true" type="danger" v-on:click="closeModal">Cancel</el-button>
			<el-button :plain="true" @click="updateForm(form)">Save</el-button>
		</div>
	</el-dialog>
</template>

<script>
	export default {
		data() {
			return {
				formLabelWidth: '120px',
				type_options: [],
			}
		},
		props: ['dialogFormVisible', 'form'],
		methods: {
			selectDemo: function (params) {
				if (params) {
					this.$axios.get("http://127.0.0.1:8000/api/persons/sex")
						.then((response) => {
							this.type_options = response.data;
							console.log(response.data);
						}).catch((response) => {
							console.log(response)
						}
					);
				}
			},
			updateForm: function (formName) {
				let itemId = formName.id;
				let phone = formName.phone;
				let email = formName.email;
				let zone = formName.zone;
				let sex = formName.sex;
				let username = formName.username;
				this.$axios.put(
					'http://127.0.0.1:8000/api/persons/detail/' + itemId,
					{
						phone,
						username,
						email,
						sex,
						zone
					}
				).then((response) => {
					console.log(response);
					this.form = response.data;
				}).catch((error) => {
					console.log(error);
				});
				location.reload();
			},
			closeModal: function () {
				this.$emit('closeModal');
			}
		}
	}
</script>
