<template>
    <q-page class="bg-grey-3 column">
        <q-list class="bg-white" separator bordered>
            <q-item
                v-for="(task, index) in tasks"
                :key="task.id"
                v-ripple
                @click="task.done = !task.done"
                :class="{ 'done bg-blue-1': task.done }"
                clickable
            >
                <q-item-section avatar>
                    <q-checkbox
                        v-model="task.done"
                        class="no-pointer-events"
                        color="primary"
                    />
                </q-item-section>
                <q-item-section>
                    <q-item-label>{{ task.title }}</q-item-label>
                </q-item-section>
                <q-item-section v-if="task.done" side>
                    <q-btn
                        flat
                        round
                        dense
                        color="primary"
                        icon="delete"
                        @click.stop="deleteTask(index)"
                    />
                </q-item-section>
            </q-item>
        </q-list>
    </q-page>
</template>

<script>
export default {
    name: "TodoPage",
    data() {
        return {
            tasks: [
                {
                    id: 1,
                    title: "Take a shower",
                    done: true,
                },
                {
                    id: 2,
                    title: "Go to work",
                    done: false,
                },
                {
                    id: 3,
                    title: "Finish work tasks",
                    done: false,
                },
                {
                    id: 4,
                    title: "Go to home",
                    done: false,
                },
            ],
        };
    },
    methods: {
        // delete task
        deleteTask(index) {
            // confirm dialog
            this.$q
                .dialog({
                    title: "Confirm",
                    message: "Are you sure ?",
                    cancel: true,
                    persistent: true,
                })
                .onOk(() => {
                    // splice task from tasks array
                    this.tasks.splice(index, 1);
                    // notify
                    this.$q.notify("Task deleted");
                });
        },
    },
};
</script>

<style lang="scss" scoped>
.done {
    .q-item__label {
        text-decoration: line-through;
        color: #bbb;
    }
}
</style>
