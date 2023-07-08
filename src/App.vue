<template>
  <div class="hello">
    <h1>Data List</h1>
    <table>
      <thead>
        <tr>
          <th>Asset name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(asset, index) in assets" :key="index">
          <td>{{ asset.name }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      assets: [
        { name: 'Printer', department: 'HR' },
        { name: 'Monitor', department: 'IT' },
        { name: 'Barcode Scanner', department: 'ACCOUNT' }
      ]
    };
  },
  methods: {
    downloadCSV() {
      const csvContent = "Asset name,Department\n" + this.assets.map(asset => `${asset.name},${asset.department}`).join("\n");
      const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
      const link = document.createElement('a');
      if (link.download !== undefined) {
        const url = URL.createObjectURL(blob);
        link.setAttribute('href', url);
        link.setAttribute('download', 'assets.csv');
        link.style.visibility = 'hidden';
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
      }
    }
  }
};
</script>

<style scoped>
table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

button {
  margin-top: 16px;
  padding: 8px 16px;
}
</style>
