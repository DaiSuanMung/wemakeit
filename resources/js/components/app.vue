<template>
        <div class="container">
            <form-wizard>
                <tab-content title="Project Title"  :before-change="validateSteps">
                    <div>
                        <div class="form-group">
                            <label for="title">Title</label>
                            <input type="text" v-model="project.title" class="form-control" aria-describedby="title" placeholder="Title">
                        </div>
                        <div class="form-group">
                            <label for="title">Intro Text</label>
                            <input type="text" v-model="project.intro" class="form-control" aria-describedby="title" placeholder="Intro Text">
                        </div>
                        <div class="form-group">
                            <label for="title">Description</label>
                            <textarea v-model="project.description" type="textarea" class="form-control" aria-describedby="title" rows="3" placeholder="Description">
                                </textarea>
                        </div>
                    </div>

                </tab-content>
                <tab-content title="Images"  :before-change="validateSteps">
                    <div class="form-group">
                        <label for="title">Image Name</label>
                        <input type="text" v-model="project.img_title" class="form-control" aria-describedby="title" placeholder="Title">
                    </div>
                    <div class="input-group mb-3">

                        <div class="custom-file mb-3">
                            <input type="file" class="custom-file-input" id="inputGroupFile01">
                            <label class="custom-file-label" for="inputGroupFile01">Choose file</label>
                        </div>

                    </div>
                    <div class="form-group">
                        <input type="text" v-model="project.img_desc" class="form-control" aria-describedby="title" placeholder="Image Description">
                    </div>
                </tab-content>
                <tab-content title="Financial Goal"  :before-change="validateSteps">
                    <div class="form-group">
                        <label for="title">Financial Goal</label>
                        <textarea type="textarea" v-model="project.goal" class="form-control" aria-describedby="title" rows="3" placeholder="Financial Goal">
                                </textarea>

                    </div>
                </tab-content>
                <tab-content title="Pledge Options"  :before-change="validateSteps">
                    <div class="form-group">
                        <label for="title">Title Money</label>
                        <input type="text" v-model="project.opt_title" class="form-control" aria-describedby="title" placeholder="Title">
                    </div>
                    <div class="form-group">
                        <label for="title">Amount of Money</label>
                        <input type="text" v-model="project.opt_amount" class="form-control" aria-describedby="title" placeholder="Amount">
                    </div>
                    <div class="form-group">
                        <label for="title">Description of what you get for your Money</label>
                        <textarea type="textarea" v-model="project.opt_desc" class="form-control" aria-describedby="title" rows="3" placeholder="Description"></textarea>
                    </div>
                </tab-content>
                <tab-content title="Set Owner Info"  :before-change="validateSteps">

                    <div class="form-group">
                        <label for="title">Adress</label>
                        <input type="text" v-model="project.adress" class="form-control" aria-describedby="title" placeholder="address">
                    </div>
                </tab-content>
            </form-wizard >
        </div>
</template>

<script>
export default {
    data(){
        return {
            step:0,
            project:{
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
            }
        }
    },

    methods:{
        validateSteps(){
            if(this.step == 0){
                if(this.project.title == '' || this.project.description == '' || this.project.intro == ''){
                    alert('error step 1 ')
                    return false;
                }
            }else if(this.step == 1) {
                if(this.project.img_title=='' || this.project.img_desc==''){
                    alert('error step 2')
                    return false;
                }
            }
            else if(this.step == 2) {
                if(this.project.goal==''){
                    alert('error step 3')
                    return false;
                }

            }
            else if(this.step == 3) {
                if(this.project.opt_title==''|| this.project.opt_amount =='' || this.project.opt_desc==''){

                    alert('error step 4')
                    return false;
                }

            }
            else if(this.step == 4) {

                if(this.project.adress==''){
                    alert('error step 5')
                    return false;
                }

            }
            this.step++;
            return true;
        },
    },




name: "app"
}
</script>

<style scoped>

</style>
