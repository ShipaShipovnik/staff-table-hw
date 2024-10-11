<template>
  <div class="wrapper">
    <aside>
      <div class="logo"><img src="./assets/media/logo.png" alt=""> Staff</div>
      <nav>
        <ul>
          <li><a href="#">Главная</a></li>
          <li><a href="#">Распорядок</a></li>
        </ul>
      </nav>
      <p class="nav-add"> <img src="./assets/media/round-green-plus-button-icon-original.svg" class="plus-icon">Добавить</p>
    </aside>
    <header>
      <h1>Список сотрудников</h1>
    </header>
    <div class="content">
      <StaffTable :staffList="staffList" :jobs="jobs" />
      <div class="form-window">
        <StaffForm @add-staff="handleAddStaff" :jobs="jobs" />
      </div>
    </div>
  </div>
</template>

<script>
import StaffTable from './components/StaffTable.vue';
import StaffForm from './components/StaffForm.vue';

export default {
  components: {
    StaffTable,
    StaffForm
  },
  data() {
    return {
      jobs: ['Менеджер', 'Администратор', 'Глава отдела', 'Бухгалтер'],
      staffList: [
        { id: '0001', name: 'Смирнова Мария Михайловна', email: '99sdhsh@gmail.com', phone: '8(836)675 98 45', job: 'Менеджер', isEdit: false },
        { id: '0002', name: 'Смирнова Антонина Михайловна', email: '99sdhsh@gmail.com', phone: '8(836)675 98 45', job: 'Бухгалтер', isEdit: false }
      ]
    };
  },
  methods: {
    handleAddStaff(newStaff) {
      const newId = (parseInt(this.staffList[this.staffList.length - 1].id) + 1).toString().padStart(4, '0');
      this.staffList.push({
        id: newId,
        ...newStaff
      });
    }
  }
};
</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>