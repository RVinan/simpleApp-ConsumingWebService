<template>
    <Page id="pageone">
        <ActionBar>
            <GridLayout>
            	<Button text="PRESS HERE TO GET MEME" @tap="onSubmit" />
            </GridLayout>
        </ActionBar>
        <GridLayout>
            <Image id="imagen" :src="urlMeme"/>
        </GridLayout>
    </Page>
</template>

<script >
import * as http from "http";
    export default {
        data() {
            return {
                urlMeme: String
            };
        },
        mounted() {
          http.getJSON("https://api.imgflip.com/get_memes").then(result => {
            this.meme = result.data.memes;
            this.urlMeme= " ";
          }, error => {
              console.log(error);
          });
        },
        
        methods: {
            onSubmit(args) {
                var rm=Math.round(Math.random() * (100 - 0)) + 0;;
                var element=this.meme[rm];
                this.urlMeme=element.url;
            }
        }    
  }
</script>

<style scoped lang="scss">
    .imagen{
        height: 80%;
        width: 100%;
    }
</style>
