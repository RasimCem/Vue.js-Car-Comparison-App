<template>
    <div class="box">
        <div class="title">
            Second Car
        </div>
        <div>
            <select  @change="clear" v-model="selected">
                <option v-for="each in car" class="select" v-bind:key="each" :value="each">{{each.make}} {{each.model}}</option>
            </select>
        </div>
        <div class="image-box">
            <img v-if="selected.length<1" class="image" src="../assets/no-car.png" alt="">
            <img v-else class="image" :src="selected.img_url" alt="">
        </div>
        <div class="car-name">
            {{selected.make}} {{selected.model}}
        </div>
        <div class="properties">
            <div class="property">
                <label>
                   Make:
                </label>
                <span>
                    {{selected.make}}
                </span>
            </div>
            <div class="property">
                <label>
                    Model:
                </label>
                <span>
                    {{selected.model}}
                </span>
            </div>
            <div class="property">
                <label>
                    Year:
                </label>
                <span>
                    {{selected.year}}
                        <i v-if="results.yearWinner==='second'" class="fas fa-check"></i>
                        <i v-if="results.yearWinner==='first'" class="fas fa-times"></i>
                </span>
            </div>
            <div class="property">
                <label>
                    Horse Power:
                </label>
                <span>
                    {{selected.horsepower}}
                        <i v-if="results.powerWinner==='second'" class="fas fa-check"></i>
                        <i v-if="results.powerWinner==='first'" class="fas fa-times"></i>
                </span>
            </div>
            <div class="property">
                <label>
                    Price:
                </label>
                <span>
                    {{selected.price}} $ 
                        <i v-if="results.priceWinner==='second'" class="fas fa-check"></i>
                        <i v-if="results.priceWinner==='first'" class="fas fa-times"></i>
                </span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['car','results'],
    data(){
        return{
            selected:''
        }
    },
     watch: {
        selected(){
            this.$emit('second',this.selected)
        }
    },
    methods:{
         clear(){
            this.$emit('clear')
        }
    }
}
</script>

<style scoped>
.title{
    font-size: 21px;
    margin: 15px 0;
    text-align: center;
}
select{
    display: block;
    margin:0 auto;
    width:80%;
    padding: 5px;
    border-radius: 3px;
    outline: none;
}
.box{
    width: 45%;
    height: auto;
    overflow: auto;
}
select:focus{
    border-color: #58677A;
}
.image-box{
    margin: 35px;
    text-align: center;
}
.image{
    width: 300px;
    height: 150px;
    border:2px solid #666;
    border-radius: 2px;
    box-shadow: 2px 2px 10px;
}
.car-name{
    font-size:19px;
    text-align: center;
    font-weight: bold;
}
.properties{
    margin:25px;
}
.property{
    margin: 8px;
}
span{
    font-weight: bold;
}
.fa-check{
    font-size: 19px;
    color:#3B7A2F;
    padding-left: 15px;
}
.fa-times{
    font-size: 19px;
    color:#C7302E;
    padding-left: 15px;
}
</style>
