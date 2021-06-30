<template>
    <div class="grid md:grid-cols-3 gap-4">
        <!-- Box 1 -->
        <div class="shadow-md bg-gray-100 p-10 text-center rounded">
            <h3 class="text-3xl text-yellow-500 font-bold mb-4">
                Cases
            </h3>
            <div class="text-2xl mb-">
                <span class="font-bold">
                    New:
                </span>{{numberWithCommas(stats.NewConfirmed)}}
            </div>
            <div class="text-2xl mb-">
                <span class="font-bold">
                    Total:
                </span>{{numberWithCommas(stats.TotalConfirmed)}}
            </div>
        </div>
        <!-- Box 2 -->
        <div class="shadow-md bg-gray-100 p-10 text-center rounded">
            <h3 class="text-3xl text-red-500 font-bold mb-4">
                Deaths
            </h3>
            <div class="text-2xl mb-">
                <span class="font-bold">
                    New:
                </span>{{numberWithCommas(stats.NewDeaths)}}
            </div>
            <div class="text-2xl mb-">
                <span class="font-bold">
                    Total:
                </span>{{numberWithCommas(stats.TotalDeaths)}}
            </div>
        </div>
        <!-- Box 3 -->
        <div class="shadow-md bg-gray-100 p-10 text-center rounded">
            <h3 class="text-3xl text-green-500 font-bold mb-4">
                Recovered
            </h3>
            <div class="text-2xl mb-">
                <span class="font-bold">
                    New:
                </span>{{numberWithCommas(stats.NewRecovered)}}
            </div>
            <div class="text-2xl mb-">
                <span class="font-bold">
                    Total:
                </span>{{numberWithCommas(stats.TotalRecovered)}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
   name: 'DataBoxes',
   props: ['stats'],
   methods: {
       numberWithCommas(x) {
           return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g,',')
       }
   }
}
</script> 