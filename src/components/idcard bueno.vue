<!-- src/components/IDCard.vue -->
<template>
  <div class="id-card-container">
    <!-- Tarjeta de identificación en la parte superior -->
    <div class="id-card">
      <div class="header">
        <div class="logo">LOGO</div>
        <h2>{{ school }}</h2>
      </div>
      <div class="profile">
        <div class="photo">[Photo]</div>
        <div class="info">
          <p>ID: {{ id }}</p>
          <p>Name: {{ studentName }}</p>
          <p>Class: {{ className }}</p>
          <p>D.O.B: {{ dob }}</p>
          <p>Address: {{ address }}</p>
          <p>Phone: {{ phone }}</p>
        </div>
      </div>
      <div class="barcode">[Barcode]</div>
      <p class="signature">Principal</p>
    </div>

    <!-- Formulario interactivo en la parte inferior -->
    <form class="id-form" @submit.prevent>
      <div class="form-group">
        <label for="school">School Name:</label>
        <input v-model="school" id="school" type="text" placeholder="Enter school name" />
      </div>

      <div class="form-group">
        <label for="id">ID:</label>
        <input v-model="id" id="id" type="text" placeholder="Enter ID" />
      </div>

      <div class="form-group">
        <label for="studentName">Student Name:</label>
        <input v-model="studentName" id="studentName" type="text" placeholder="Enter student name" />
      </div>

      <div class="form-group">
        <label for="className">Class Name:</label>
        <input v-model="className" id="className" type="text" placeholder="Enter class name" />
      </div>

      <div class="form-group">
        <label for="dob">Date of Birth:</label>
        <input v-model="dob" id="dob" type="date" />
      </div>

      <div class="form-group">
        <label for="address">Address:</label>
        <input v-model="address" id="address" type="text" placeholder="Enter address" />
      </div>

      <div class="form-group">
        <label for="phone">Phone:</label>
        <input v-model="phone" id="phone" type="text" placeholder="Enter phone number" />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'IDCard',
  data() {
    return {
      school: '',
      id: '',
      studentName: '',
      className: '',
      dob: '',
      address: '',
      phone: ''
    };
  }
};
</script>

<style scoped>
.id-card-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.id-card {
  border: 1px solid #000;
  padding: 16px;
  margin-bottom: 20px;
  width: 350px;
  background-color: #f0f4f8;
  font-family: Arial, sans-serif;
}

.header {
  display: flex;
  align-items: center;
  background-color: #b3e5c8;
  padding: 10px;
}

.header h2 {
  color: #333; /* Color del título para mejorar la visibilidad */
}

.logo {
  background-color: #ffffff;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  margin-right: 10px;
}

.profile {
  display: flex;
  margin-top: 10px;
}

.photo {
  width: 80px;
  height: 80px;
  background-color: #e0e0e0;
  margin-right: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.info p {
  margin: 5px 0;
  line-height: 1.2;
  color: #333; /* Color de texto para mejorar la legibilidad */
}

.barcode {
  margin-top: 15px;
  text-align: center;
  font-size: 12px;
  background-color: #e0e0e0;
  height: 30px;
}

.signature {
  text-align: right;
  font-style: italic;
  margin-top: 10px;
  color: #333; /* Color de la firma */
}

.id-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;
  max-width: 350px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
}

input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
