<tempplate>
  <div :class="{ dynamic: subject.length > 3}">
  <h2>{{ title }}<h2>
    <form @submit.prevent="addNewSubject">
      <label> Enter new subject: </label>
      <input v-model="newSubject" />
      <button>Add Subject</button>
    </form>
    <hr />
    <ul>
      <li v-for="(item, index) in subjects" key="index">
        {{ item.content }}
        <button @click="deleteSubject(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
    props: {
      title: { type: String, required: true},
    },
    setup() {
    const newSubject = ref('zö');
    const subjects = ref([]);

    function addNewSubject() {
      //console.log('addNewSubject ' + newSubject.value);
      subjects.value.push({
        content: newSubject.value,
      });
      newSubject.value = '';
      console.log(subjects.value);
    }

    function deleteSubject(index) {
      console.log('delete');
      subjects.value.splice(index, 1);
    }

    return { newSubject, addNewSubject, subjects, deleteSubject };
  },
};
</script>
<style scoped>
  h3 {
    margin-bottom: 20px;
  }
  hr {
    margin-top: 20px;
    margin-bottom: 20px;
  }
  .dynamic{
    color: green;
  }
</style>