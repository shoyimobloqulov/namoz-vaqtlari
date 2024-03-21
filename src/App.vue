<script>
    import axios from 'axios';

    export default {
        data() {
            return {
                apiData: '',
                regions: '',
                region: 'Samarqand',
                data: '',
            }
        },
        methods: {
            getRegion() {
                axios.get('https://islomapi.uz/api/present/day?region='+this.region.split(' ')[0])
                .then(response => {
                    this.apiData = response.data;
                })
                .catch(error => {});
            }
        },
        mounted() {
            axios.get("https://robocontest.uz/api/regions")
                .then(response => {
                    this.regions = response.data;
                })
                .catch(error => {});
            
            axios.get('https://islomapi.uz/api/present/day?region='+this.region)
                .then(response => {
                    this.apiData = response.data;
                })
                .catch(error => {});
        }
    }
</script>

<template>
    <div class="row container mx-auto mt-3">
        <div class="col-md-9">
            {{ region }} / {{ apiData.date }} / {{  apiData.weekday }}
        </div>
        <div class="col-md-3">
            <div class="form-group">
                <select v-on:change='getRegion' v-model="region" class="form-control select2">
                    <option v-for="x in regions" :value="x.name" :key="x.id">{{ x.name }}</option>
                </select>
            </div>
        </div>
    </div>
    <div class="content">
        <div class="row container m-3" v-if="apiData">
            <div class="col-md-2">
                <div class="body-circle">
                    <div class="circle">
                        <div class="circle-text">
                            <h5 class="time">{{ apiData.times.tong_saharlik }}</h5>
                            <p>Тонг</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-2">
                <div class="body-circle">
                    <div class="circle active">
                        <div class="circle-text">
                            <h5 class="time">{{ apiData.times.quyosh }}</h5>
                            <p>Қуёш</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-2">
                <div class="body-circle">
                    <div class="circle">
                        <div class="circle-text">
                            <h5 class="time">{{ apiData.times.peshin }}</h5>
                            <p>Пешин</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-2">
                <div class="body-circle">
                    <div class="circle">
                        <div class="circle-text">
                            <h5 class="time">{{ apiData.times.asr }}</h5>
                            <p>Аср</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-2">
                <div class="body-circle">
                    <div class="circle">
                        <div class="circle-text">
                            <h5 class="time">{{ apiData.times.shom_iftor }}</h5>
                            <p>Шом</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-2">
                <div class="body-circle">
                    <div class="circle">
                        <div class="circle-text">
                            <h5 class="time">{{ apiData.times.hufton }}</h5>
                            <p>Хуфтон</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
</style>