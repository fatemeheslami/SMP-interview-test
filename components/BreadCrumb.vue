<template>
    <div>
        <v-breadcrumbs :items="items">
            <template v-slot:divider>
                <v-icon>mdi-chevron-left</v-icon>
            </template>
        </v-breadcrumbs>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items:[
                {
                    text: 'خانه'
                }
            ]
        }
    },
    props: {
        breadCrumb: {
            type: Object,
            default: () => { },
        },
    },
    mounted() {
        const firstBred = {}
        const secondBread = {}
        firstBred.text = this.breadCrumb?.child?.title
        secondBread.text = this.breadCrumb?.child?.child?.title
        this.items.push(firstBred)
        this.items.push(secondBread)

    }
}
</script>

<style>
 .v-breadcrumbs li {
    color: #4A5F73;
    cursor: pointer;
    font-size: 16px;
}
</style>