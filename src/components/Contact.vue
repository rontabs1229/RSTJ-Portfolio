<template>
	<div class="container mb-5" id="contact">
		<div class="row">
			<div class="col py-5">
				<h2>Contact</h2>
			</div>
		</div>
		<div class="row mt-3 px-5" id="map">
			<div class="col-12 col-md-6 my-auto">
				<img src="/images/map.png" class="img-fluid justify-content-center mb-5">
			</div>
			<form @submit.prevent="submitForm" class="col-12 col-md-6 ms-auto mb-5" id="form_section">
				<div>
				<div class="mb-3">
				  <label for="nameInput" class="form-label" id="name_label">Name:</label>
				  <input type="text" v-model="name" class="form-control" id="nameInput" placeholder="Enter Full Name" required>
				</div>

				<div class="mb-3">
				  <label for="companyInput" class="form-label" id="name_label">Company:</label>
				  <input type="text" v-model="company" class="form-control" id="companyInput" placeholder="Company Name" required>
				</div>

				<div class="mb-3">
				  <label for="emailInput" class="form-label" id="email_label">Email Address:</label>
				  <input type="email" v-model="email" class="form-control" id="emailInput" placeholder="name@example.com" required>
				</div>
				<div class="mb-3">
				  <label for="messageInput" class="form-label" id="message_label">Message:</label>
				  <textarea class="form-control" v-model="message" id="messageInput" rows="5" placeholder="Connect with RSTJ" required></textarea>
				</div>
				<button id="contact-submit-btn" type="submit" class="btn mb-3" :disabled="isLoading">{{ isLoading ? "Sending..." : "Submit" }}</button>
			</div>
			</form>
		</div>
	</div>
</template>

<script setup>
	import { ref } from 'vue';
	import { Notyf } from 'notyf';
	import 'notyf/notyf.min.css';

	const notyf = new Notyf();
	const WEB3FORMS_ACCESS_KEY = "43a8bf8a-8132-43f9-b222-fcf2df97912a";
	const subject = "New message from Portfolio Form";

	const name = ref("");
	const company = ref("");
	const email = ref("");
	const message = ref("");
	const isLoading = ref(false);

	const submitForm = async () => {
		isLoading.value = true;
		try {
			const response = await fetch("https://api.web3forms.com/submit", {
				method: "POST",
				headers: {
					"Content-Type": "application/json",
					Accept: "application/json",
				},
				body: JSON.stringify({
					access_key: WEB3FORMS_ACCESS_KEY,
					subject: subject,
					name: name.value,
					company: company.value,
					email: email.value,
					message: message.value,
				})
			});

			const result = await response.json();

			if (result.success) {
				console.log(result);
				notyf.success("Message Sent to RSTJ!");
				name.value = "";
				company.value = "";
				email.value = "";
				message.value = "";
			} else {
				console.log(result);
				notyf.error(result.message || "Failed to send message.");
			}
		} catch (error) {
			console.log(error);
			notyf.error("Failed to send message.");
		} finally {
			isLoading.value = false;
		}
	}
</script>