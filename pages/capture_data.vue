<template>
  <div>
    <span>Multiline message is:</span>
    <p style="white-space: pre-line">{{ text_value }}</p>
    <textarea v-model="text_value" placeholder="add multiple lines"></textarea>
    <br/><button @click="process_text">Procesar texto</button>
    <!--img :src="img_url" v-if="img_url" alt="AI Image" /-->
    <p>{{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const text_value = ref("");
const img_url = ref(null);
const result = ref('');

async function query(data) {
  const response = await fetch("https://api-inference.huggingface.co/models/mistralai/Mistral-7B-v0.1", {
    headers: { Authorization: "Bearer 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" },
			method: "POST",
			body: JSON.stringify([{"role": "user", "content": "What is the bash command to list all files in a folder and sort them by last modification?"}]
),
  });
  console.log('Response',response)
/*  if (response.ok) {
    
    //const blob = await response.blob();
    // Create a URL for the blob (assuming it's an image)
    //img_url.value = URL.createObjectURL(blob);
  } else {
    // Handle error here
    console.error("Error");
  }*/
}


const process_text = () => {
  query({"inputs":text_value }).then((response) => {
    console.log(JSON.stringify(response));
  });
};
</script>

<style scoped></style>
