<template>
  <div>
    <div>
      <v-form @submit.prevent="submit" class="form_auth">
        <h2 class="headline font-weight-bold my-3">What's your project info?</h2>
        <v-layout align-center>
          <v-text-field name="login"
                        class="child-flex"
                        label="Enter the URL for your workspace"
                        v-model="subdomain"
                        type="text"
                        autofocus
                        outline
                        v-validate="{required: true, max: 21, regex: /[a-zA-Z0-9-]+$/}"
                        data-vv-name="subdomain"
                        :error-messages="errors.collect('subdomain')"
                        required></v-text-field>
          <label class="title font-weight-bold ml-1">
            .satlegal.io
          </label>
        </v-layout>
        <v-btn :loading="submitting"
               :disabled="submitting || !subdomain"
               @click="submit" color="primary" class="ml-0">Next
          <v-icon right dark>arrow_forward</v-icon>
        </v-btn>
        <div class="subheading mt-3">
          Or,
          <router-link class="link_bt" :to="{ name: 'signin' }">Sign In workspace?</router-link>
        </div>
      </v-form>

      <SetSubdomainToken
        :token="token"
        :subdomain="subdomain"
        :load="iframeLoaded"
      />
    </div>
  </div>
</template>

<script>
  import slugify from "slugify";
  import {getSubdomainURL} from "../../utils/index";
  import {setSubdomains} from "../../store/modules/auth";
  import SetSubdomainToken from "./SetSubdomainToken";

  export default {
    name: "CreateWorkSpace",
    components: {SetSubdomainToken},
    $_veeValidate: {
      validator: 'new'
    },
    data: () => ({
      subdomain: "",
      token: "",
      submitting: false,
      formError: "",
      dictionary: {
        custom: {
          subdomain: {
            required: () => 'Sub domain code can not be empty',
            max: 'The name field need entered 21 characters',
            regex: 'The field name not enter special characters',
            // custom messages
          }
        }
      },

    }),
    mounted() {
      this.$validator.localize('en', this.dictionary)
    },
    props: {
      email: {
        type: String,
        required: true
      },
      code: {
        type: String,
        required: true
      }
    },
    watch: {
      name(value) {
        this.subdomain = slugify(value)
          .toLowerCase()
          .replace(/^-+|-+$/g, "")
          .slice(0, 21);
      }
    },
    methods: {
      iframeLoaded() {
        this.submitting = false;
        let subdomainURL = getSubdomainURL(this.subdomain);
        location.href = `${subdomainURL}/invite-members`;

      },
      submit() {
        let {email, code, subdomain} = this;
        this.formError = [];
        this.snackbar = false;
        if (!this.subdomain) {
          this.snackbar = true;
          this.formError = "Please enter your workspace url";
          return false;
        }
        this.submitting = true;
        this.$http
          .post("/api/users/auth/create-workspace/", {email, code, name: subdomain})
          .then(response => {
            let _token = response.data.token;
            this.subdomain = response.data.workspace;
            this.token = _token;
            setSubdomains(response.data.workspace);
          })
          .catch((error) => {
            this.submitting = false;
            if (error.response.status === 400) {
              if (error.response.data["name"]) {
                this.snackbar = true;
                this.formError = error.response.data["name"].toString();
                this.$eventHub.$emit(this.$eventTypes.snackNotify, error.response.data["name"].toString())
              } else {
                this.$eventHub.$emit(this.$eventTypes.snackNotify, "")
                // location.reload(); // TODO: ...
              }
            }
          });
      }
    }
  }
</script>

<style scoped>
  .flex_label {
    /*border: solid 1px red;*/
    display: flex;
    justify-content: space-between;
    align-items: center;

  }

  .flex_label ._title {
    flex: 1;
  }

  .flex_label ._icon {
    font-family: 'Roboto', sans-serif !important;
    background: #4caf50;
    padding: 4px 10px 2px 10px;
    margin-left: 0px;
    color: #fff;
    text-align: center;
    font-size: 16px;
  }
</style>
