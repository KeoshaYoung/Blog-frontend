<script>
export default {
  data: function () {
    return {
      message: "Contact Info",
      email: "Blog@example.com",
      phoneNumber: "(706)123-4567",
      mailingAddress: "Blog Author 123 Mountain Dr Augusta, GA 30909",
    };
  },
};
</script>

<template>
  <h2>{{ message }}</h2>
  <p>{{ email }}</p>
  <p>{{ phoneNumber }}</p>
  <p>{{ mailingAddress }}</p>
</template>
