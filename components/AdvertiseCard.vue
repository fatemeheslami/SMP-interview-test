<template>
    <div style="padding: 10px">
        <v-card>
            <v-card-text>
                <div class="d-flex justify-space-between">
                    <div>
                        <NuxtLink class="link" to="#">
                            {{ advertise[0]?.name }}
                        </NuxtLink>
                        <div>
                            <p class="gray--text mt-5">
                                {{
                                    `${advertise[0]?.relativeTime} در ${advertise[0]?.city?.name} - ${advertise[0]?.city?.name}`
                                }}
                            </p>
                        </div>
                        <div class="d-flex">
                            <div class="ml-5">
                                <span>7
                                    <v-icon>mdi-eye-outline</v-icon>
                                </span>
                            </div>
                            <div>
                                <v-icon>mdi-message-outline</v-icon>
                            </div>
                        </div>
                    </div>
                    <div>
                        <v-img :src="advertise[0]?.mainImage?.fileUrl" width="100"></v-img>
                    </div>
                </div>
            </v-card-text>
        </v-card>
    </div>
</template>

<script>
export default {
    props: {
        advertise: {
            type: Array,
            default: () => [],
        },
    },
};
</script>

<style scoped>
.link {
    text-decoration: none;
    color: #222;
    font-size: 16px;
}
</style>
