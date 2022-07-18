<template>
    <q-page class="bg-grey-3 column">
        <div class="row q-pa-sm bg-primary">
            <q-input
                v-model="newTask"
                @keyup.enter="addTask"
                class="col"
                square
                filled
                bg-color="white"
                placeholder="Add Task"
                dense
            >
                <template v-slot:append>
                    <q-btn @click="addTask" round dense flat icon="add" />
                </template>
            </q-input>
        </div>
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
        <div class="no-tasks absolute-center" v-if="!tasks.length">
            <q-icon name="check" size="100px" color="primary" />
            <div class="text-h5 text-primary text-center">No tasks</div>
        </div>
    </q-page>
</template>

<script>
export default {
    name: "TodoPage",
    data() {
        return {
            // tasks array
            tasks: [
                // {
                //     id: 1,
                //     title: "Take a shower",
                //     done: true,
                // },
                // {
                //     id: 2,
                //     title: "Go to work",
                //     done: false,
                // },
                // {
                //     id: 3,
                //     title: "Finish work tasks",
                //     done: false,
                // },
                // {
                //     id: 4,
                //     title: "Go to home",
                //     done: false,
                // },
            ],

            // new task
            newTask: "",
        };
    },
    methods: {
        // add new task
        addTask() {
            // push new task to tasks array
            this.tasks.push({
                title: this.newTask,
                done: false,
            });
            // notify
            this.$q.notify("Task added");
            // reset new task
            this.newTask = "";
        },

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

.no-tasks {
    opacity: 0.5;
}
</style>
