
<template>
    <Shell>
        <div class="grid gap-10 p-10">
            <h1 class="text-4xl py-4 font-bold">Power Outages in Mauritius</h1>
            <!-- My Awesome tab -->
             <div  class="flex gap-4">
                <div v-for="tab in tabs" >
                    <button @click="changeTab(tab)" class="bg-white rounded-md p-3" :class="currentTab === tab ? 'bg-cyan-700 text-white' : 'bg-white'">{{ tab }}</button>
                </div>
             </div>
            <!-- <h2 class="text-2xl font-bold">C</h2> -->

            <div v-for="item in current">
                <CardsPicked :outage="item"/>
            </div>
            
            <!-- <h2 class="text-2xl font-bold">Tomorrow</h2> -->

            <!-- <div v-for="item in future">
                <CardsPicked :outage="item"/>
            </div> -->

        </div>
    </Shell>
</template>

<script setup>
  
const API_ENDPOINT = 'https://raw.githubusercontent.com/MrSunshyne/mauritius-dataset-electricity/main/data/power-outages.latest.json'

async function fetchJson(url = API_ENDPOINT) {
    try {
        const response = await fetch(url)
        return response.json()
    }
    catch (error) {
        throw new Error(`Error fetching JSON: ${error}`)
    }
}

const mydata = await fetchJson()

const tabs = ['today', 'future']
const currentTab = ref('today')

function changeTab(tab) {
    currentTab.value = tab
}

const today = mydata.today
const future = mydata.future

const current = computed(() => {
    return mydata[currentTab.value]
})
</script>