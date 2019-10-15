<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 col-md-offset-3">
        <h3>VueJS ile gelen Directive Tanımları</h3>
        <p v-text="'Deneme yanilma metodu her zaman iyidir..'"></p>
        <p v-html="'<strong>Bu da v-html</strong>'"></p>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6 col-md-offset-3">
        <h3>Custom Directive</h3>
        <p v-animate.delay.flash="{mainColor : 'green' , secondColor : 'blue' , delay : 500 }">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores aspernatur beatae culpa doloribus, ex
          facilis fugiat, fugit magni molestiae mollitia, nesciunt nihil perspiciatis quaerat quam quas ratione sequi
          unde ut!</p>
      </div>
      <div class="col-md-6 col-md-offset-3">
        <h3>Custom Directive</h3>
        <p v-animate:background.delay="'yellow'">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores aspernatur beatae culpa doloribus, ex
          facilis fugiat, fugit magni molestiae mollitia, nesciunt nihil perspiciatis quaerat quam quas ratione sequi
          unde ut!</p>
      </div>
      <div class="col-md-6 col-md-offset-3">
        <h3>Custom-on directive</h3>
        <p v-custom-on:click="methos">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Asperiores aspernatur beatae culpa doloribus, ex
          facilis fugiat, fugit magni molestiae mollitia, nesciunt nihil perspiciatis quaerat quam quas ratione sequi
          unde ut!</p>
          <button v-custom-on:click="metos">Tıklandı</button>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    directives : {
      "color" : {
        bind(el,binding,vnode){
         let delay = 0 ;
         if(binding.modifiers["delay"]){
           delay = 2000;
         }
         if(binding.modifiers["flash"]){
           let firstColor = binding.value;
           let secondColor = "#fbbd08";
           let currentColor = firstColor;

           setTimeout(()=>{
             setInterval(()=>{
             currentColor == secondColor ? currentColor = firstColor : currentColor = secondColor;
             if(binding.arg == "background"){
             el.style.backgroundColor = currentColor;
           }else{
             el.style.color = currentColor;
           }
           },1000)
         }, delay)
         }else{
           setTimeout(()=>{
           if(binding.arg == "background"){
             el.style.backgroundColor = binding.value
           }else{
             el.style.color = binding.value
           }
         }, delay)
      }
      }
    },
    "animate" : {
      bind(el,binding,vnode){
        let delay = 0;
        if(binding.modifiers["delay"]){
          delay = 2000;
        }
        
        if(binding.modifiers["flash"]){
              let firstColor = binding.value.mainColor;
              let secondColor = binding.value.secondColor;
              let currentColor = firstColor;
          setTimeout(()=>{
            setInterval(()=>{
              currentColor == firstColor ? currentColor = secondColor : currentColor = firstColor;
              if(binding.arg == "background"){
                el.style.backgroundColor = currentColor
              }else {
                el.style.color = currentColor
              }
            },binding.value.delay)
          },delay)
        }else {
          setTimeout(()=>{
            if(binding.arg == "background"){
                el.style.backgroundColor = binding.value
              }else {
                el.style.color = binding.value
              }
          },delay)
        }
      }
    },
    "custom-on" : {
      bind(el,binding,vnode){
        let argument = binding.arg;
        let value = binding.value;
       el.addEventListener(argument,value);
      }
    },
  },
  methods : {
    metos(){
      alert("Tıklandı...!!!")
    }
  }
  }
</script>

<style>

</style>
