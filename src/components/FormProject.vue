<template>
  <div>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
    >
    <input type="search" v-model="searchQuery" placeholder="Search...">
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">First</th>
          <th scope="col">Last</th>
          <th scope="col">Email</th>
          <th scope="col">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(person, index) in filteredPeople" :key="index">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ person.firstName }}</td>
          <td>{{ person.lastName }}</td>
          <td>{{ person.email }}</td>
          <td>
            <span v-if="person.gender === 'M'" class="gender-male">M</span>
            <span v-if="person.gender === 'F'" class="gender-female">F</span>
          </td>
          <td>
            <button class="btn btn-danger" @click="deletePerson(index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "FormProject",
  data() {
    return {
      searchQuery: "",
      people: [
        { firstName: "chhin", lastName: "keo", email: "keo@gmail.com", gender: "M" },
        { firstName: "meng", lastName: "korng", email: "korng@gmail.com", gender: "F" },
        { firstName: "thi", lastName: "reach", email: "reach@gmail.com", gender: "M" },
      ],
    };
  },
  computed: {
    filteredPeople() {
      return this.people.filter((person) => {
        const fullName = `${person.firstName} ${person.lastName}`;
        return fullName.toLowerCase().includes(this.searchQuery.toLowerCase());
      });
    },
  },
  methods: {
    deletePerson(index) {
      this.people.splice(index, 1);
    },
  },
};
</script>

<style>
.gender-male {
  color: green;
}

.gender-female {
  color: red;
}
</style>