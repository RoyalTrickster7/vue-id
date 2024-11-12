<template>
  <div class="id-card-container">
    <div class="id-card">
      <div class="header">
        <img class="logo" src="/src/assets/logo.png" alt="School Logo" />
        <h2>{{ school }}</h2>
      </div>
      <div class="profile">
        <div class="photo">
          <img :src="photoUrl" alt="Student Photo" />
        </div>
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

      <!-- Botón de carga para la foto -->
      <div class="form-group">
        <label for="photo">Upload Photo:</label>
        <input type="file" id="photo" @change="openCropper" />
      </div>
    </form>

    <!-- Modal para Cropper -->
    <div v-if="showCropper" class="modal">
      <div class="modal-content">
        <h3>Adjust and Crop your Photo</h3>
        <img ref="cropperImage" :src="photoUrl" alt="Crop Image" />
        <button @click="cropImage">Crop & Save</button>
        <button @click="closeCropper">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
import Cropper from 'cropperjs';
import 'cropperjs/dist/cropper.css';

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
      phone: '',
      photoUrl: 'https://via.placeholder.com/80',
      showCropper: false,
      cropper: null
    };
  },
  methods: {
    openCropper(event) {
      const file = event.target.files[0];
      if (file) {
        this.photoUrl = URL.createObjectURL(file);
        this.showCropper = true;
        this.$nextTick(() => {
          this.cropper = new Cropper(this.$refs.cropperImage, {
            aspectRatio: 1,
            viewMode: 1
          });
        });
      }
    },
    cropImage() {
      if (this.cropper) {
        const canvas = this.cropper.getCroppedCanvas({
          width: 80,
          height: 80
        });
        this.photoUrl = canvas.toDataURL('image/png');
        this.cropper.destroy();
        this.cropper = null;
        this.showCropper = false;
      }
    },
    closeCropper() {
      if (this.cropper) {
        this.cropper.destroy();
        this.cropper = null;
      }
      this.showCropper = false;
    }
  }
};
</script>

<style>
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
  color: #333;
}

.header {
  display: flex;
  align-items: center;
  background-color: #b3e5c8;
  padding: 10px;
}

.logo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 10px;
}

.profile {
  display: flex;
  margin-top: 10px;
}

.photo img {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 4px;
}

.info p {
  margin: 5px 0;
  line-height: 1.2;
  color: #333;
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
  color: #333;
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

/* Estilos del modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  width: 90%;
  max-width: 400px;
}

.modal-content img {
  max-width: 100%;
  height: auto;
}
</style>
