<template>
  <div>
    <div class="container">
        <div class="line_bar"></div>
        <div class="line">
            <div id="activeStep1" class="dot zero"><span class="dot_num">1</span></div>
            <div id="activeStep2" class="dot center"><span class="dot_num">2</span></div>
            <div id="activeStep3" class="dot full"><span class="dot_num">3</span></div>
            <div id="activeStep4" class="dot full2"><span class="dot_num">4</span></div>
        </div>

        <div class="steps">
            <div class="step step-one">
                <div class="liner"></div>
                <span id="activeStep1_span">Step1</span>
            </div>
            <div class="step step-two">
                <div class="liner"></div>
                <span id="activeStep2_span">Step2</span>
            </div>
            <div class="step step-three">
                <div class="liner"></div>
                <span id="activeStep3_span">Step3</span>
            </div>
            <div class="step step-four">
                <div class="liner"></div>
                <span id="activeStep4_span">Step4</span>
            </div>
        </div>
        <div class="col-md-2 content_div">
                <input style="margin-top: 60px;margin-left: -40px;" v-model="stepOne" type="text">
                <span style="color:red" v-if="$v.stepOne.$dirty && !$v.stepOne.required">Enter text</span>
        </div>
        <div class="col-md-3 content_div">
            <div v-if="isStep2">
                <input  style="margin-top: 60px" v-model="stepTwo" type="text">
                <span  style="color:red" v-if="$v.stepTwo.$dirty && !$v.stepTwo.required">Enter text</span>
            </div>
            <button type="button" class="btn btn-primary btn_nxt" v-if="isStep1" @click="onStep1Next()">Next</button>
        </div>
        <div class="col-md-3 content_div">
            <div v-if="isStep3">
                <input  style="margin-top: 60px" v-model="stepThree" type="text">
                <span  style="color:red" v-if="$v.stepThree.$dirty && !$v.stepThree.required">Enter text</span>
            </div>
            <button type="button" class="btn btn-primary btn_nxt" v-if="isStep2 && !isStep3" @click="onStep2Next()">Next</button>
        </div>
         <div class="col-md-3 content_div_last">
            <button type="button" class="btn btn-primary btn_nxt" v-if="isStep3" @click="onFinish()">Save</button>
        </div>

        </div>
    </div>
</template>

<script>
import $ from 'jquery'
import { required } from 'vuelidate/lib/validators'
export default {
  name: 'BaseComponent',
  props: {
    
  },
  data() {
    return {
        isStep1:true,
        isStep2 :false,
        isStep3 :false,
        stepOne:'',
        stepTwo:'',
        stepThree:''

    }
  },
  validations(){
        return {
            stepOne :{
                required
            },
            stepTwo:{
                required
            },
            stepThree:{
                required
            }
        }
  },
  computed:{
      
  },
  methods:{
      onStep1Next(){
         this.$v.stepOne.$touch()
         if(this.$v.stepOne.$error == false){
          this.isStep1 = false,   
          this.isStep2 = true
           $('#activeStep2').css({
                    'background': '#ff0099',
                    'opacity': 1
            })
            $('#activeStep2_span').css({
                    'color': '#ff0099',
            })
             $('#activeStep1').css({
                    'background': '#999',
                    'opacity': 1
            })
            $('#activeStep1_span').css({
                    'color': '#999',
                    'opacity': 1
            })
        } 
      },
      onStep2Next(){
         this.$v.stepTwo.$touch()
         if(this.$v.stepTwo.$error == false){
          this.isStep1 = false,   
          this.isStep2 = true,
          this.isStep3 = true
           $('#activeStep3').css({
                    'background': '#ff0099',
                    'opacity': 1
            })
            $('#activeStep2').css({
                    'background': '#999',
                    'opacity': 1
            })
             $('#activeStep1').css({
                    'background': '#999',
                    'opacity': 1
            })
            $('#activeStep3_span').css({
                    'color': '#ff0099',
            })
            $('#activeStep2_span').css({
                    'color': '#999'
            })
             $('#activeStep1_span').css({
                    'color': '#999',
            })
        } 
      },
      onFinish(){
          this.$v.stepThree.$touch()
         if(this.$v.stepThree.$error == false){
          this.isStep1 = false,   
          this.isStep2 = true,
          this.isStep3 = true
          this.$toast.open({
                message: 'Task Completed',
                position: 'top',
                type: 'success',
                // all of other options may go here
            });
           $('#activeStep4').css({
                    'background': '#ff0099',
                    'opacity': 1
            })
            $('#activeStep3').css({
                    'background': '#999',
                    'opacity': 1
            })
            $('#activeStep2').css({
                    'background': '#999',
                    'opacity': 1
            })
             $('#activeStep4_span').css({
                    'color': '#ff0099',
                    'opacity': 1
            })
             $('#activeStep1').css({
                    'background': '#999',
                    'opacity': 1
            })
            $('#activeStep3_span').css({
                    'color': '#999',
            })
            $('#activeStep2_span').css({
                    'color': '#999'
            })
             $('#activeStep1_span').css({
                    'color': '#999',
            })
        } 
      }
  }
  
}
</script>

<style scoped>
.container {
  width: 700px;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}

.steps {
  margin-bottom: 10px;
  position: relative;
  height: 25px;
}

.steps > div {
  position: absolute;
  top: 0;
  -webkit-transform: translate(-50%);
  -ms-transform: translate(-50%);
  transform: translate(-50%);
  height: 25px;
  padding: 0 5px;;
  display: inline-block;
  width: 80px;
  text-align: center;
  -webkit-transition: .3s all ease;
  transition: .3s all ease;
}

.steps > div > span {
  line-height: 25px;
  height: 25px;
  margin: 0;
  color: #777;
  font-family: 'Roboto', sans-serif;
  font-size: .9rem;
  font-weight: 300;
}

.steps > div > .liner {
  position: absolute;
  height: 2px;
  width: 0%;
  left: 0;
  top: 50%;
  margin-top: -1px;
  background: #999;
  -webkit-transition: .3s all ease;
  transition: .3s all ease;
}

.step-one {
  left: 0;
}

.step-two {
  left: 30%;
}

.step-three {
  left: 54%;
}
.step-four {
  left: 80%;
}

.line {
  width: 80%;
  height: 2px;
  background: #9e9a9a;
  position: relative;
  border-radius: 10px;
  overflow: visible;
  margin-bottom: 7px;
}

.line .dot-move {
  position: absolute;
  top: 50%;
  left: 0%;
  width: 15px;
  height: 15px;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  background: #ddd;
  border-radius: 50%;
  -webkit-transition: .3s all ease;
  transition: .3s all ease;
}

.line .dot {
  position: absolute;
  top: 50%;
  width: 50px;
  height: 50px;
  left: 0;
  background: #ddd;
  border-radius: 50%;
  -webkit-transition: .3s all ease;
  transition: .3s all ease;
  -webkit-transform: translate(-50%, -50%) scale(.5);
  -ms-transform: translate(-50%, -50%) scale(.5);
  transform: translate(-50%, -50%) scale(.5);
}

.line .dot.zero {
  left: 0%;
  background: #ff0099;
}



.line .dot.center {
  left: 38%;
  background: #bbb
}

.line .dot.full {
  left: 68%;
  background: #bbb
}
.line .dot.full2 {
  left: 100%;
  background: #bbb
}
.dot_num{
    padding-left: 17px;
    color: white;
    font-size: 30px;
}
.line_bar{
    width: 85%;
    height: 45px;
    position: absolute;
    top: -12px;
    background: #ddd;
    left: -15px;
}
.content_div{
    height:300px;
    margin-top: -42px;
    border-right: 2px solid #9e9a9a;
}
.content_div_last{
    height:300px;
    margin-top: -42px;
}
.btn_nxt{
    margin : 60px 0 0 30px;
}
#activeStep1_span{
    color:#ff0099;
}
</style>
