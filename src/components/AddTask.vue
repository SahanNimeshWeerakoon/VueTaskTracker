<template>
<form @submit="addTask" class="add-form">
    <div class="form-control">
        <label>Task</label>
        <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
        <label>Day & Time</label>
        <input type="text" v-model="day" name="day" placeholder="Add Day & Time" />
    </div>
    <div class="form-control label">
        <label>Set Reminder</label>
        <input type="checkbox" v-model="reminder" name="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
</form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            text: '',
            day: '',
            reminder: false
        };
    },
    methods: {
        addTask(e) {
            e.preventDefault();
            if(!this.text) {
                alert('Please add text');
                return;
            }

            const newTask = {
                id: Math.floor(Math.random() * 100000),
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }

            this.$emit('add-task', newTask);

            this.text = '';
            this.day = '';
            this.reminder = false;
        }
    }
}
</script>

<style scope>
    .add-form, .add-form .form-control,  .add-form .form-control label,  .add-form .form-control input, input {
        width: 100%;
    }
    .add-form .form-control {
        margin-bottom: 20px;
    }
    .add-form .form-control input {
        padding: 5px 0px;   
    }
    .add-form .form-control.label {
        display: flex;
    }
    .add-form .form-control.label label, .add-form .form-control.label input {
        width: 50%;
    }
    input[type="submit"] {
        background: #000;
        color: #fff;
        padding: 10px 0;
    }
</style>