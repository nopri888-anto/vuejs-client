<template>
  <div class="row justify-content-center">
    <div class="col-8">
      <router-link
        :to="{ name: 'transaction.create' }"
        class="btn btn-primary btn-sm rounded shadow mb-3"
        >Add</router-link
      >

      <div class="card rounded shadow">
        <div class="card-header">Transaction List</div>
        <div class="card-body">
          <table class="table">
            <thead>
              <tr>
                <th>Title</th>
                <th>Amounts</th>
                <th>Type</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(transaction, index) in transactions.data"
                :key="index"
              >
                <td>{{ transaction.title }}</td>
                <td>{{ transaction.amount }}</td>
                <td>{{ transaction.type }}</td>
                <td>
                  <div class="btn-group">
                    <router-link
                      :to="{
                        name: 'transaction.edit',
                        params: { id: transaction.id },
                      }"
                      class="btn btn-sm btn-outline-info"
                      >Edit
                    </router-link>
                    <button class="btn btn-sm btn-outline-danger">
                      Delete
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { onMounted, ref } from "vue";

export default {
  async setup() {
    const transactions = ref([]);

    onMounted(() => {
      //get data api endpoint
      axios
        .get("http://127.0.0.1:8000/api/transaction")
        .then((result) => {
          transactions.value = result.data;
        })
        .catch((err) => {
          console.log(err.response.message);
        });
    });

    return {
      transactions,
    };
  },
};
</script>