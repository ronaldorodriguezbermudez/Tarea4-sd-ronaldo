<template>
  <div class="container">
    <h2>Login</h2>
    <form @submit="login">
      <div class="form-group">
        <input type="text" v-model="formData.username" placeholder="Enter Username">
      </div>
      <div class="form-group">
        <input type="password" v-model="formData.password" placeholder="Enter Password">
      </div>
      <div class="form-group">
        <button class="button button-primary" type="submit" > Login </button>
      </div>
    </form>
  </div>
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
        async login(event){
            event.preventDefault();
            
            try {
                const response = await fetch('https://tarea4-sd-ronaldo.netlify.app/.netlify/functions/login', {
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
  


