<template>
    <table>
        <thead>
            <tr>
                <th>Табличный номер</th>
                <th>ФИО</th>
                <th>Почта</th>
                <th>Телефон</th>
                <th>Должность</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="staff in staffList" :key="staff.id">
                <template v-if="!staff.isEdit">
                    <td>{{ staff.id }}</td>
                    <td>{{ staff.name }}</td>
                    <td>{{ staff.email }}</td>
                    <td>{{ staff.phone }}</td>
                    <td>{{ staff.job }}</td>
                    <td>
                        <button @click="editStaff(staff)" class="table-btns edit">Редактировать</button> <br>
                        <button @click="deleteStaff(staff)" class="table-btns delete">Удалить</button>
                    </td>
                </template>
                <template v-if="staff.isEdit">
                    <td><input type="text" v-model="staff.id" placeholder="Таблич.номер" class="table-edit-input"></td>
                    <td><input type="text" v-model="staff.name" placeholder="ФИО" class="table-edit-input"></td>
                    <td><input type="email" v-model="staff.email" placeholder="Почта" class="table-edit-input"></td>
                    <td><input type="text" v-model="staff.phone" placeholder="Телефон" class="table-edit-input"></td>
                    <td><select v-model="staff.job" class="table-edit-input">
                            <option value="" disabled selected>Выберите должность</option>
                            <option v-for="job in jobs" :key="job">{{ job }}</option>
                        </select>
                    </td>
                    <td>
                        <button @click="saveStaff(staff)" class="table-btns edit" >Сохранить</button><br>
                        <button @click="deleteStaff(staff)" class="table-btns delete">Удалить</button>
                    </td>
                </template>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: {
        staffList: {
            type: Array,
            required: true
        },
        jobs: {
            type: Array,
            required: true
        }
    },
    methods: {
        deleteStaff(staff) {
            const index = this.staffList.indexOf(staff);
            if (index !== -1) {
                this.staffList.splice(index, 1);
            }
        },
        saveStaff(staff) {
            staff.isEdit = false;
        },
        editStaff(staff) {
            staff.isEdit = true;
        }
    }
};
</script>

<style scoped>
table {
    width: 100%;
    border-collapse: collapse;
}

th,
td {
    border: 1px solid #ddd;
    padding: 8px;
}

th {
    background-color: #f2f2f2;
}
</style>