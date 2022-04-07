<template>
  <section>
    
    <v-alert
      :value="alert"
      color="pink"
      dark
      border="top"
      transition="scale-transition"
      id="status"
    >
    </v-alert>

      <form @submit.prevent="sendForm" action="https://formspree.io/f/xyyojqkw" method="post" id="form">
    <v-text-field
      name="name"
      v-model="value.name"
      label="Name"
    ></v-text-field>
    <v-text-field
      name="email"
      v-model="value.email"
      label="E-mail"
    ></v-text-field>
    <v-container fluid>
      <v-textarea
        name="message"
        v-model="value.message"
        clearable
        clear-icon="mdi-close-circle"
        label="Text"
      ></v-textarea>
    </v-container>
    <v-btn
      type="submit"
      class="mr-4"
    >
      submit
    </v-btn>
    <v-btn>
      clear
    </v-btn>
  </form>
  </section>

</template>

<script>
  export default {
    
   data: () => ({
      value: {
      name: 'Test',
      email: 'ramusassogba@gmail.com',
      message: 'Ceci est un méssage',
      },
      alert: false
    }),

    methods: {
      async sendForm (e) {
        var status = document.getElementById("status");
        e.preventDefault()
        const currentObj = this
        const res = await fetch('https://formspree.io/f/xwkybdvz', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(
          {...this.value}
        )
        }).then(function (response) {
          currentObj.output = response.data
          status.innerHTML = "Thanks for your submission!";
        }).catch(function (error) {
          currentObj.output = error
        })
      },

      
      handleSubmit(value) {
       var data = new FormData(value);
        var status = document.getElementById("status");
        fetch('https://formspree.io/f/xyyojqkw', {
          method: 'post',
          body: data,
        }).then(response => {
          if (response.ok) {
            status.innerHTML = "Thanks for your submission!";
          } else {
            response.json().then(data => {
              if (Object.hasOwn(data, 'errors')) {
                status.innerHTML = data["errors"].map(error => error["message"]).join(", ")
              } else {
                status.innerHTML = "Oops! There was a problem submitting your form"
              }
            })
          }
        }).catch(error => {
          status.innerHTML = "Oops! There was a problem submitting your form"
        });
      }
    },

    async mounted () {
      
    },
  }
</script>