<template>
	<div>
		<div class="formitem-container">
			<div class="label-container">
				<label for="first_name">First Name:</label>
			</div>
			<div class="input-container">
				<input
					type="text"
					id="first_name"
					:class="validationInputClass"
					v-model="first_name"
					@input="updateModel"
				>
				<div
					:class="validationIconClass">
				</div>
			</div>

		</div>
		<div
			:class="validationMsgClass">
			<div
				v-for="error in errors"
				>
				{{ error }}
			</div>
		</div>
	</div>
</template>

<script>
/* eslint-disable */

export default {
	data () {
		return {
			first_name: null,
			errors: null
		}
	},
	computed: {
		validationInputClass() {
			if(this.errors == null) {
				return 'unvalidatedInput'
			}
			else if(this.errors){
				if(this.errors.length > 0) {
					return 'validatedInput invalid';
				}
				else {
					return 'validatedInput valid';
				}
			}
		},
		validationMsgClass() {
			if(this.errors == null) {
				return 'unvalidatedMsgContainer'
			}
			else if(this.errors){
				if(this.errors.length > 0) {
					return 'validatedMsgContainer invalid';
				}
				else {
					return 'unvalidatedMsgContainer valid';
				}
			}
		},
		validationIconClass() {
			if(this.errors == null) {
				return 'validationIcon unvalidated'
			}
			else if(this.errors){
				if(this.errors.length > 0) {
					return 'validationIcon invalid';
				}
				else {
					return 'validationIcon valid';
				}
			}
		},
	},
	methods: {
		updateModel() {
			this.errors = [];
			if(this.first_name == '') {
				this.errors.push('This field is required');
			}
			if (this.invalidCharValidation() === true) {
				this.errors.push('Numbers, special characters and spaces not allowed')
			}

			this.$emit('input', this.first_name);
		},
		invalidCharValidation() {
			var invalidChars = "0123456789 <>@!#$%^&*()_+[]{}?:;|'\"\\,./~`-=";
			var i;
			for (i=0; i < invalidChars.length ; i++) {
				if (this.first_name.includes(invalidChars[i])) {
					return true;
				}
			}
		}
	}
}
</script>
