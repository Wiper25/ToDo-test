<template>
  <div class="list">
    <div class="list__empty-block">
      <div class="list__to-do-list">
        <h5>Список дел</h5>
      </div>
      <div class="list__block">
        <h4 class="list__empty" v-if="!cards">Пусто</h4>
        <table v-if="cards">
          <tr>
            <td>
              <b-button @click="sortExecution" class="list__btn-group"
                >По выполнению</b-button
              >
            </td>
            <td>
              <b-button @click="sortTitle()" class="list__btn-group"
                >По названию</b-button
              >
            </td>
            <td>
              <b-button @click="sortID" class="list__btn-group"
                >По номеру</b-button
              >
            </td>
            <td>
              <b-button @click="sortPriority" class="list__btn-group"
                >По приоритету</b-button
              >
            </td>
            <td>
              <b-button @click="sortColor" class="list__btn-group"
                >По цвету</b-button
              >
            </td>
          </tr>
          <tr :key="i" v-for="(card, i) in cards">
            <td>
              <b-button
                class="list__btn-group"
                @click="card.status = !card.status"
                >{{ card.status ? "Открыть" : "Закрыть" }}</b-button
              >
            </td>
            <td :class="{ done: card.status }">{{ card.title }}</td>
            <td :class="{ done: card.status }">{{ card.description }}</td>
            <td :class="{ done: card.status }">
              <h6 v-if="card.importance == 'A'">Высокий</h6>
              <h6 v-if="card.importance == 'B'">Средний</h6>
              <h6 v-if="card.importance == 'C'">Низкий</h6>
            </td>
            <td>
              <div
                style="width: 100%; height: 10px; margin: 0 auto"
                :style="`background-color:${card.colorCard}`"
              ></div>
            </td>
          </tr>
        </table>
      </div>
    </div>

    <div class="text-center my-3">
      <b-button
        v-b-popover.hover="'Все записи будут стерты.'"
        href="/list"
        @click="clear()"
        title="ВНИМАНИЕ!!!"
        >Очистить</b-button
      >
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cards: JSON.parse(localStorage.getItem("card")),
    };
  },
  methods: {
    clear() {
      localStorage.clear();
    },
    sortExecution() {
      this.cards.sort(function (a, b) {
        let statusA = a.status,
          statusB = b.status;
        if (statusA < statusB) return -1;
        if (statusA > statusB) return 1;
        return 0;
      });
    },
    sortTitle() {
      this.cards.sort(function (a, b) {
        let titleA = a.title.toLowerCase(),
          titleB = b.title.toLowerCase();
        if (titleA < titleB) return -1;
        if (titleA > titleB) return 1;
        return 0;
      });
    },
    sortID() {
      this.cards.reverse();
    },
    sortPriority() {
      this.cards.sort(function (a, b) {
        let importanceA = a.importance.toLowerCase(),
          importanceB = b.importance.toLowerCase();
        if (importanceA < importanceB) return -1;
        if (importanceA > importanceB) return 1;
        return 0;
      });
    },
    sortColor() {
      this.cards.sort(function (a, b) {
        let colorCardA = a.colorCard.toLowerCase(),
          colorCardB = b.colorCard.toLowerCase();
        if (colorCardA < colorCardB) return -1;
        if (colorCardA > colorCardB) return 1;
        return 0;
      });
    },
  },
  beforeDestroy() {},
};
</script>
<style scoped>
.list__to-do-list {
  background-color: #9e9e9e;
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}
.list__empty-block {
}
table {
  width: 100%;
  border: 1px solid gray;
  margin: 0px 0px 0px 0px;
}
tr {
}
td {
  width: 20%;
  border: 1px solid white;
  word-wrap: break-word;
}
h5 {
  margin: 0;
  color: #5a5656;
}
h6 {
  margin: 0;
}
.list__btn-group {
  width: 100%;
}
.list__block {
  display: flex;
  flex-direction: column;
}
.list__card {
  width: 20%;
  margin: 20px;
}
.list__marker {
  width: 95%;
  height: 10px;
  margin: 0 auto;
  border-top-right-radius: 20px;
  border-top-left-radius: 20px;
}
.list__gruop {
  display: block;
  margin: 0 auto;
}
.done {
  text-decoration: line-through;
  color: black;
}
.list__empty-block {
  background-color: #cfcece;
  border-radius: 20px;
  padding-bottom: 10px;
  margin-top: 20px;
  text-align: center;
}

.list__empty {
  margin: 10px;
  color: rgb(90, 86, 86);
}
</style>
