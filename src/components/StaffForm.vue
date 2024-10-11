<template>
    <h1>Новый сотрудник</h1>
    <form @submit.prevent="addStaff" class="staff-form">
        <input type="text" v-model="newStaff.name" placeholder="ФИО" class="form-inputs">
        <input type="email" v-model="newStaff.email" placeholder="Почта" class="form-inputs">
        <input type="text" v-model="newStaff.phone" placeholder="Телефон" class="form-inputs">
        <select v-model="newStaff.job" class="form-inputs">
            <option value="" disabled selected>Выберите должность</option>
            <option v-for="job in jobs" :key="job">{{ job }}</option>
        </select><br>
        <button type="submit" class="add-btn">Добавить</button>
        <p v-if="error" class="error">{{ error }}</p>
    </form>
</template>

<script>
export default {
    props: {
        jobs: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            newStaff: {
                name: '',
                email: '',
                phone: '',
                job: ''
            },
            error: ''
        };
    },
    methods: {
        addStaff() {
            if (this.newStaff.name.trim() === '') {
                this.error = 'Введите имя';
            } else if (this.newStaff.email.trim() === '') {
                this.error = 'Почта не введена';
            } else if (this.newStaff.phone.trim() === '') {
                this.error = 'Телефон не введен';
            } else if (this.newStaff.job.trim() === '') {
                this.error = 'Должность не введена';
            } else {
                this.$emit('add-staff', this.newStaff);
                this.newStaff = {
                    name: '',
                    email: '',
                    phone: '',
                    job: '',
                    isEdit: false,
                };
                this.error = '';
            }
        }
    }
};
</script>

<style scoped>
.error {
    color: red;
}
</style>