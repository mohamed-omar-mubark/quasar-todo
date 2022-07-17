<template>
    <q-layout view="lHh Lpr lFf">
        <q-header>
            <q-toolbar>
                <q-btn
                    flat
                    dense
                    round
                    @click="leftDrawerOpen = !leftDrawerOpen"
                    icon="menu"
                    aria-label="Menu"
                />
            </q-toolbar>
            <div class="q-px-lg q-pt-xl q-mb-md">
                <div class="text-h3">Todo</div>
                <div class="text-subtitle1">{{ todysDate }}</div>
            </div>
            <q-img
                src="../assets/mountains.jpg"
                class="header-image absolute-top"
            />
        </q-header>

        <q-drawer
            v-model="leftDrawerOpen"
            show-if-above
            :width="250"
            :breakpoint="600"
        >
            <q-scroll-area
                style="
                    height: calc(100% - 192px);
                    margin-top: 192px;
                    border-right: 1px solid #ddd;
                "
            >
                <q-list padding>
                    <q-item to="/" exact clickable v-ripple>
                        <q-item-section avatar>
                            <q-icon name="list" />
                        </q-item-section>

                        <q-item-section> Todo </q-item-section>
                    </q-item>

                    <q-item to="/help" exact clickable v-ripple>
                        <q-item-section avatar>
                            <q-icon name="help" />
                        </q-item-section>

                        <q-item-section> Help </q-item-section>
                    </q-item>
                </q-list>
            </q-scroll-area>

            <q-img
                class="absolute-top"
                src="../assets/mountains.jpg"
                style="height: 192px"
            >
                <div class="absolute-bottom bg-transparent">
                    <q-avatar size="56px" class="q-mb-sm">
                        <img
                            src="https://avatars.githubusercontent.com/u/88965473?v=4"
                        />
                    </q-avatar>
                    <div class="text-weight-bold">Mohamed Omar</div>
                    <div>@mohamed.omar</div>
                </div>
            </q-img>
        </q-drawer>

        <q-page-container>
            <heep-alive>
                <router-view />
            </heep-alive>
        </q-page-container>
    </q-layout>
</template>

<script>
import { date } from "quasar";

export default {
    name: "MainLayout",

    data() {
        return {
            leftDrawerOpen: false,
        };
    },

    computed: {
        todysDate() {
            const timeStamp = Date.now();
            return date.formatDate(timeStamp, "dddd D MMMM");
        },
    },
};
</script>

<style lang="scss" scoped>
.header-image {
    height: 100%;
    z-index: -1;
    opacity: 0.1;
    filter: grayScale(100%);
}
</style>
