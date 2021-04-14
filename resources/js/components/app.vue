<template>

        <div class="container">

            <div class="alert alert-success" v-if="isCompleted">
                <h1>Project Created !</h1>
                <button @click="ShowCreateProject">Create Projects</button>
            </div>

    <div>
        <button @click="changeLang('en')">en</button>
        <button @click="changeLang('de')">de</button>
    </div>
            <form-wizard  @on-complete="createProject" v-if="!isCompleted">




                <tab-content title="Project Title"  :before-change="validateSteps">
                    <div>
                        <div class="form-group">
                            <label for="title">{{this.chLang == 'en' ? this.lang.en.title : this.lang.de.title}}</label>
                            <input type="text"  v-model="form.title" class="form-control "
                                   :class="{ 'is-invalid': form.errors.has('title') }"
                                   aria-describedby="title" placeholder="Title">
                            <has-error :form="form" field="title"></has-error>


                        </div>
                        <div class="form-group">
                            <label for="title">Intro Text</label>
                            <input type="text" v-model="form.intro"
                                   :class="{ 'is-invalid': form.errors.has('intro') }"
                                   class="form-control" aria-describedby="title" placeholder="Intro Text">
                                    <has-error :form="form" field="intro"></has-error>
                        </div>
                        <div class="form-group">
                            <label for="title">Description</label>
                            <textarea v-model="form.description"
                                      :class="{ 'is-invalid': form.errors.has('description') }" type="textarea"
                                      class="form-control" aria-describedby="title" rows="3" placeholder="Description">
                                </textarea>
                            <has-error :form="form" field="description"></has-error>
                        </div>
                    </div>

                </tab-content>
                <tab-content title="Images"  :before-change="validateSteps">
                    <div class="form-group">
                        <label for="title">Image Name</label>
                        <input type="text" v-model="form.img_title"
                               :class="{ 'is-invalid': form.errors.has('img_title') }"
                               class="form-control" aria-describedby="title" placeholder="Title">
                            <has-error :form="form" field="img-title"></has-error>
                    </div>
                    <div class="input-group mb-3">

                        <div class="custom-file mb-3">
                            <input type="file" @change="uploadImage" class="custom-file-input" id="inputGroupFile01">
                            <label class="custom-file-label" for="inputGroupFile01">Choose file</label>
                        </div>

                    </div>
                    <div class="form-group">
                        <input type="text" v-model="form.img_desc"
                               :class="{ 'is-invalid': form.errors.has('img_desc') }"
                               class="form-control" aria-describedby="title" placeholder="Image Description">
                        <has-error :form="form" field="img_desc"></has-error>
                    </div>
                </tab-content>
                <tab-content title="Financial Goal"  :before-change="validateSteps">
                    <div class="form-group">
                        <label for="title">Financial Goal</label>
                        <textarea type="textarea" v-model="form.goal"
                                  :class="{ 'is-invalid': form.errors.has('goal') }"
                                  class="form-control" aria-describedby="title" rows="3" placeholder="Financial Goal">
                                </textarea>
                        <has-error :form="form" field="goal"></has-error>

                    </div>
                </tab-content>
                <tab-content title="Pledge Options"  :before-change="validateSteps">
                    <div class="form-group">
                        <label for="title">Title Money</label>
                        <input type="text" v-model="form.opt_title"
                               :class="{ 'is-invalid': form.errors.has('opt_title') }"
                               class="form-control" aria-describedby="title" placeholder="Title">
                                <has-error :form="form" field="opt_title"></has-error>
                    </div>
                    <div class="form-group">
                        <label for="title">Amount of Money</label>
                        <input type="number" v-model="form.opt_amount"
                               :class="{ 'is-invalid': form.errors.has('opt_amount') }"
                               class="form-control" aria-describedby="title" placeholder="Amount">
                                <has-error :form="form" field="opt_amount"></has-error>
                    </div>
                    <div class="form-group">
                        <label for="title">Description of what you get for your Money</label>
                        <textarea type="textarea" v-model="form.opt_desc"
                                  :class="{ 'is-invalid': form.errors.has('opt_desc') }"
                                  class="form-control" aria-describedby="title" rows="3" placeholder="Description"></textarea>
                                <has-error :form="form" field="opt_desc"></has-error>
                    </div>
                </tab-content>
                <tab-content title="Set Owner Info"  :before-change="validateSteps">

                    <div class="form-group">
                        <label for="title">Adress</label>
                        <input type="text" v-model="form.adress"
                               :class="{ 'is-invalid': form.errors.has('adress') }"
                               class="form-control" aria-describedby="title" placeholder="address">
                        <has-error :form="form" field="adress"></has-error>
                    </div>
                </tab-content>
            </form-wizard >
        </div>
</template>

<script>
import { Form, HasError, AlertError } from 'vform'

Vue.component(HasError.name, HasError)
Vue.component(AlertError.name, AlertError)
export default {

    data(){
        return {
            chLang:'en',
            lang:{
                en:{
                   title:'title',

                },
                de:{
                    title:'titel'
                }
            },
            step:0,
            isCompleted:false,
            erros:[],
            form: new Form({
                //step1
                title:'',
                intro: '',
                description:'',
                //step2
                img_title: '',
                img:'',
                img_desc:'',
                //step3
                goal:'',
                //step4
                opt_title:'',
                opt_amount:'',
                opt_desc:'',
                //step5
                adress:'',
            }),

        }
    },


    methods:{
        createProject(){
            this.form.post('/api/create/project')
                .then(({ response }) => {
                    console.log(response)
                    this.isCompleted = true;

                })

        },
        uploadImage(event){
            let file = event.target.files[0]
            let reader = new FileReader();
            reader.onloadend = (file) => {
                this.form.img = reader.result;
            }
            reader.readAsDataURL(file)
        },
        ShowCreateProject(){
          this.isCompleted = false;
          this.form = new Form({
              //step1
              title:'',
              intro: '',
              description:'',
              //step2
              img_title: '',
              img:'',
              img_desc:'',
              //step3
              goal:'',
              //step4
              opt_title:'',
              opt_amount:'',
              opt_desc:'',
              //step5
              adress:'',
          });

        },
        changeLang(lang){
            this.chLang = lang
        },
        validateSteps(){
           return true;
        },
    },




name: "app"
}
</script>

<style scoped>

</style>
