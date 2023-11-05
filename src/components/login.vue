<template>
    <form @submit.prevent="submitForm">
      <h2>Login</h2>
      <div class="input-field">
        <input type="text" v-model="formData.username" placeholder="Enter Username">
      </div>
      <div class="input-field">
        <input type="password" v-model="formData.password" placeholder="Enter Password">
      </div>
      <input type="submit" value="LogIn">
    </form>
  </template>
  
  <script>
export default {
  data() {
    return {
      formData: {
        username: "",
        password: "",
      },
    };
  },
    
    methods: {
        async Login(event){
            event.preventDefault();
            try {
                const response = await fetch('http://tarea4-sd-ronaldo.netlify.app/.netlify/funtions/login', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(this.formData),
                });

                if (response.status === 200) {
                    const data = await response.json();
                    // Guarda el token en una cookie en lugar de localStorage
                    document.cookie = `token=${data.token};path=/`;
                    this.$router.push("/home");
                } else {
                    console.error('Error de autenticación');
                }
                } catch (error) {
                    console.error(error);
                }
    },
  },
};  
</script>
  


