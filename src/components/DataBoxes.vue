<template>
    <div class="grid md:grid-cols-2 gap-4">
        <div class="flex flex-col items-center justify-center bg-blue-300">
            <h3>Cases</h3>
            <div><span class="font-bold">New:</span>{{ addThousandSeparator(stats.NewConfirmed) }}</div>
            <div><span class="font-bold">Total:</span>{{ addThousandSeparator(stats.TotalConfirmed) }}</div>
        </div>
        <div class="flex flex-col items-center justify-center bg-blue-300">
            <h3>Deaths</h3>
            <div><span class="font-bold">New:</span>{{ addThousandSeparator(stats.NewDeaths) }}</div>
            <div><span class="font-bold">Total:</span>{{ addThousandSeparator(stats.TotalDeaths) }}</div>
        </div>
    </div>
</template>
<script>
export default {
    name: "DataBoxes",
    props: ["stats"],
    methods: {
        addThousandSeparator(number) {
            return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
        },
    },
};
</script>
<style scoped></style>
