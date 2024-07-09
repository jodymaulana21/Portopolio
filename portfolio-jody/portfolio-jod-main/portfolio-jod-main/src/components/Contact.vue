<template>
  <div
    class="py-4 p-st"
    :class="{
      'bg-light': !nightMode,
      'bg-dark2': nightMode,
      'text-light': nightMode,
    }"
  >
    <div class="container">
      <div
        class="text-center"
        data-aos="fade"
        data-aos-once="true"
        data-aos-duration="1000"
      >
        <span
          class="title text-center"
          :class="{ pgray: !nightMode, 'text-light': nightMode }"
          >Contact.</span
        >
      </div>
      <hr
        width="50%"
        :class="{ pgray: !nightMode, 'bg-secondary': nightMode }"
      />
      <br />
      <div class="row justify-content-center">
        <div
          class="col-xl-4 col-bg-4 col-md-4 col-sm-12 text-center pb-6 px-5"
          data-aos="fade-up"
          data-aos-once="true"
          data-aos-duration="1000"
          @click="open('whatsapp')"
        >
          <div class="bg-div"><i class="fab fa-whatsapp"></i></div>
          <br/>
          <span class="title2">{{ "08986513543" }}</span>
        </div>

        <div
          class="col-xl-4 col-bg-4 col-md-4 col-sm-12 text-center pb-6 px-5"
          data-aos="fade-up"
          data-aos-once="true"
          data-aos-duration="1000"
          @click="open('linkedin')"
        >
          <div class="bg-div"><i class="fab fa-linkedin"></i></div>
            <br/>
          <span class="title2">{{ "Jody Maulana" }}</span>
        </div>

        <div
          class="col-xl-4 col-bg-4 col-md-4 col-sm-12 text-center pb-6 px-5"
          data-aos="fade-up"
          data-aos-once="true"
          data-aos-duration="1000"
          @click="open('instagram')"
        >
          <div class="bg-div"><i class="fab fa-instagram"></i></div>
            <br/>
          <span class="title2">{{ "@jody_maulana" }}</span>
        </div>

        <div
          class="col-xl-4 col-bg-4 col-md-4 col-sm-12 text-center pb-6 px-5"
          data-aos="fade-up"
          data-aos-once="true"
          data-aos-duration="1000"
        >
          <div class="bg-div"><i class="fa fa-at"></i></div>
          <br/>
          <span class="title2">{{ "jody_maulana21@gmail.com" }}</span>
        </div>

        
      </div>

      <Snackbar
        :showSnackbar="showSnackbar"
        @close="closeSnackbar"
        :snackbarMessage="snackbarMessage"
        :snackbarColor="snackbarColor"
      />
    </div>
  </div>
</template>

<script>
import config from "../../config";
import emailjs from "emailjs-com";
import info from "../../info";

import Snackbar from "./helpers/Snackbar";

export default {
  name: "Contact",
  components: {
    Snackbar,
  },
  props: {
    nightMode: {
      type: Boolean,
    },
  },
  data() {
    return {
      email: "",
      name: "",
      text: "",
      showSnackbar: false,
      snackbarMessage: "",
      snackbarColor: "",
      linkedin: info.links.linkedin,
      instagram: info.links.instagram,
      whatsapp: info.links.whatsapp
      
    };
    
  },
  methods: {
    open(link) {
      switch (link) {
        case "linkedin":
          window.open(this.linkedin, "_blank");
          break;
        case "github":
          window.open(this.github, "_blank");
          break;
        case "figma":
          window.open(this.figma, "_blank");
          break;
        case "resume":
          window.open(this.resume, "_blank");
          break;
        case "instagram":
          window.open(this.instagram, "_blank");
          break;
        case "whatsapp":
          window.open(this.whatsapp, "_blank");
          break;
      }
    },
    closeSnackbar(val) {
      if (!val) {
        setTimeout(() => {
          this.showSnackbar = val;
        }, 1000);
      }
    },
    sendEmail() {
      if (!this.email || !this.name || !this.text) {
        this.showSnackbar = true;
        this.snackbarMessage = "Please all the fields";
        this.snackbarColor = "#64808E";
      } else {
        var obj = {
          user_email: this.email,
          from_name: this.name,
          message_html: this.text,
          to_name: "Mahy Mohab",
        };

        emailjs
          .send(
            config.emailjs.serviceID,
            config.emailjs.templateID,
            obj,
            config.emailjs.userID
          )
          .then(
            (result) => {
              this.showSnackbar = true;
              this.snackbarMessage = "Thanks! Message recieved.";
              this.snackbarColor = "#1aa260";

              this.email = "";
              this.text = "";
              this.name = "";
            },
            (error) => {
              this.showSnackbar = true;
              this.snackbarMessage = "Oops! Something went wrong.";
              this.snackbarColor = "#64808E";
            }
          );
      }
    },
  },
};
</script>

<style scoped>
.title {
  font-size: 30px;
  font-weight: 500;
}
.title1 {
  font-size: 24px;
  font-weight: 400;
}

.title2 {
  font-size: 20px;
  font-weight: 400;
}

.title3 {
  font-size: 16px;
  font-weight: 400;
}

.pinput {
  font-size: 18px;
  outline: none;
  border: none;
  border-radius: 7px;
  padding: 10px;
  width: 50%;
  transition: all 1s;
  background-color: #b3b3cc;
}

.btn {
  border-color: #759CC9;
  color: #759CC9;
  width: 50%;
}

.btn:hover {
  background-color: #759CC9;
  border-color: #759CC9;
  color: white;
}

.btn:focus {
  background-color: #759CC9;
  border-color: #759CC9;
  color: white;
}

.pgray-dark {
  background-color: #3c4148 !important;
}

@media screen and (max-width: 1000px) {
  .pinput {
    width: 90%;
  }
  .pinput {
    width: 90%;
  }

  .btn {
    width: 90%;
  }
}
</style>
