<template>
  <v-app id="inspire" :dark="isDark">
    <v-content>
      <v-container fluid fill-height pa-0>
        <v-layout justify-start align-center>
          <v-flex xs12 sm8 md6 pa-3>
            <router-view></router-view>
          </v-flex>
          <v-flex xs12 sm4 md6 fill-height>
            <div class="fill-height bg_grd">
              <div class="pos-r-t">
                <v-tooltip bottom>
                  <v-btn icon target="_blank" slot="activator">
                    <v-switch v-model="isDark"></v-switch>
                  </v-btn>
                  <span>{{isDark ? 'Bright' : 'Dark'}}</span>
                </v-tooltip>
              </div>
              <v-container fill-height>
                <v-layout align-center>
                  <v-flex text-xs-center>
                    <LogoAuth/>
                  </v-flex>
                </v-layout>
              </v-container>
            </div>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
    <Snack/>
  </v-app>

</template>
<script>
  import Snack from '../components/utils/Snack'
  import LogoAuth from "../components/auth/LogoAuth";

  export default {
    name: "NotLoggedIn",
    components: {LogoAuth, Snack},
    data() {
      return {
        isDark: false,
        gradient: 'to top right, rgba(63,81,181, .7), rgba(25,32,72, .7)'
      }
    }
  };
</script>

<style>
  body {
    background: -webkit-gradient(linear, right top, left bottom, from(#e85b48), color-stop(#e73a65), color-stop(#b12caa), to(#6d42c7));
    background: linear-gradient(to left bottom, #e85b48, #e73a65, #b12caa, #6d42c7);
  }

  .auth-wrapper {
    background-image: url("data:image/png;base64,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GBVaHFGtFwlR0oGS+1+QDgpcTJqJkd53gtHKz+1f2pLcvF1vnfZgy1Nnyi35hDonb19XMGUvbRmhJLfPD3P7/LjnTsnPbpS2LJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSfvd02oOnmWfasneawZbSlORZXmapE02ZoSRJ90aSRJJEkkSSJJIkkiSSJJIkkSSRJJEkkSSJJIkkiSSJJEkkSSRJJEkiSSJJIkkiSRJJEkkSSRJJkkiSSJL+r6TSEZotmPfIgzh/tlw6JedNVmlL8gl9dErOSs2vTunVF5fIDnOJ7LgTXSLbt06DJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiSSSSCKJJJJIIokkkkgiiaSf3jttwdNcS1tWsGVcOs1gyyptSSSNTtdgyvzsNENJku6NJIkkiSSJJEkkSSRJJEkkSSJJIkkiSSJJEkkSSRJJEkmSSJIe2Tdal8rJoQy0ywAAAABJRU5ErkJggg==");
    background-size: auto;
    background-repeat: repeat;
    background-position: 0 0;
  }

  .auth-wrapper .theme--light.application {
    background: none;
  }

  .bg_grd {
    background-color: rgb(51, 51, 51);
    /*background-color: rgba(109, 66, 199, 1);*/
    position: relative;
    overflow: hidden;
  }

  .bg_grd:before {
    content: '';
    display: block;
    z-index: 0;
    position: absolute;
    background-color: rgb(40, 40, 40);
    /*background-color: rgba(255, 255, 255, 0.3);*/
    left: 36.5%;
    top: -42px;
    transform: rotate(15deg);
    width: 27%;
    height: 115%;
  }
  .pos-r-t {
    position: absolute;
    top: 0px;
    right: 0px;
  }
  .link_bt {
    text-decoration: none;
    /*font-size: 1rem;*/
  }
  .form_auth {
    /*border: solid 1px red;*/
    max-width: 480px;
    width: 100%;
    margin: 0 auto;
  }
</style>
