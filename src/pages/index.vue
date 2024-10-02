<template>
    <div>
        <h1>Who is this</h1>
        
        <Spinner v-if="loading" />
        <Picture v-else :itemID="id" :showPicture="showPicture"/>

        <Options :options="options" :disabled="disabled" @selected="optionSelected"/>
        <!-- <input type="number" v-model="id">
        <button @click="getOptionsIDs">get options</button> -->
    </div>
  </template>
  
  <script>
  import Picture from '@/components/Picture';
  import Options from '@/components/Options';
  import Spinner from '@/components/Spinner';
  import api from '@/utilities/api'

  export default {
    components: { Picture, Options, Spinner},
    data () {
        return {
            id: 1,
            options: [],
            optionsQuantity: 5,
            max: 100,
            loading: false,
            disabled: false,
            showPicture: false,
            taken: [],
        }
    },
    beforeMount(){
        this.getOptionsIDs();
    },
    methods: {
        getRandom(min, max, taken){
            const n = Math.floor(Math.random() * (max - min + 1)) + min;
            return taken?.includes(n) ? this.getRandom(min, max, taken) : n;
        },

        async getOptionsIDs(){
            this.loading = true;
            this.disabled = false;
            this.showPicture = false;
            
            this.options = [];
            while (this.options.length < this.optionsQuantity) {
                let taken = [...this.taken, ...this.options.map(x=>x.id)];
                this.options.push({id: this.getRandom(1, this.max, taken)});
            }
            await this.formatOptions();
            this.id = this.options[this.getRandom(0, this.optionsQuantity-1)].id;
            if (this.max - this.taken.length < 10) this.taken = [];
            this.taken.push(this.id);
            this.loading = false;
        },

        async formatOptions(){
            for (let option of this.options) {
                option.name = await this.getOptionName(option.id);
            }
        },

        async getOptionName(id) {
            const res = await api.get(`/${id}`);
            return res?.data?.name || "";
        },

        async optionSelected(option) {
            option.correct = option.id === this.id;
            option.disabled = true;
            if (option.correct) {
                this.disabled = true;
                this.showPicture = true;
                await new Promise((res)=>setTimeout(res, 1000))
                for (const option of this.options.filter(x=>!x.correct)) {
                    option.name = null;
                    await new Promise((res)=>setTimeout(res, 300))
                }
                setTimeout(() => {
                    this.loading = true;
                }, 500);
                setTimeout(() => {
                    this.getOptionsIDs()
                }, 1000);
            }
        }
    }
  }
  </script>
  

  