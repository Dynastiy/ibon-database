<template>
  <div class="">
    <div class="user_onboarding_wrap">
      <h5 class="font-weight-bold">Personal Details</h5>

      <div class="registration_wrap mt-3">
        <form action="" @submit.prevent="updateProfile">
          <div class="row">
            <div class="col-md-12">
              <div class="d-flex align-items-center justify-content-between">
                <div class="d-flex align-items-center" style="gap: 30px">
                  <div class="profile_photo">
                    <img
                      v-if="dataObj.profile"
                      :src="
                        baseUrl +
                        dataObj.profile.profile_photo +
                        '?' +
                        Date.now()
                      "
                      alt=""
                      srcset=""
                    />
                  </div>
                  <div class="center">
                    <div class="form-input2">
                      <div class="preview">
                        <img id="file-ip-1-preview" />
                      </div>
                      <label for="file-ip-1" id="update">Update Photo</label>

                      <input
                        type="file"
                        id="file-ip-1"
                        accept="image/*"
                        @change="showPreview($event)"
                      />
                    </div>
                    <div class="upload" id="upload-file" @click="uploadPhoto">
                      <button>Upload</button>
                    </div>
                  </div>
                </div>

                <div class="update_password">
                  <div class="upload">
                    <button @click="update_password = !update_password">Update Password</button>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">First Name</label>
                <input
                  v-model="dataObj.first_name"
                  type="text"
                  class="form-control"
                  placeholder="First Name"
                />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">Last Name</label>
                <input
                  v-model="dataObj.last_name"
                  type="text"
                  class="form-control"
                  placeholder="Last Name"
                />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">Work Email</label>
                <input
                  v-model="dataObj.email"
                  type="text"
                  class="form-control"
                  placeholder="Email"
                />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">Phone Number</label>
                <input
                  v-model="dataObj.profile.phone_number"
                  type="tel"
                  class="form-control"
                  placeholder="Phone Number"
                />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">Date of Birth</label>
                <input
                  v-model="dataObj.profile.date_of_birth"
                  type="date"
                  class="form-control"
                  placeholder="dd-mm-yy"
                />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >Gender</label
                >
                <select
                  class="form-control option-class select"
                  id="exampleFormControlSelect1"
                  v-model="dataObj.profile.gender"
                >
                  <option value="">---</option>
                  <option class="colour" value="Male" id="selectCountry">
                    Male
                  </option>
                  <option class="colour" value="Female" id="selectCountry">
                    Female
                  </option>
                </select>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >Marital Status</label
                >
                <select
                  v-model="dataObj.profile.marital_status"
                  class="form-control option-class select"
                  id="exampleFormControlSelect1"
                >
                  <option value="">---</option>
                  <option class="colour" value="Single" id="selectCountry">
                    Single
                  </option>
                  <option class="colour" value="Married" id="selectCountry">
                    Married
                  </option>
                  <option class="colour" value="Divorced" id="selectCountry">
                    Divorced
                  </option>
                </select>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >Religion</label
                >
                <select
                  v-model="dataObj.profile.religion"
                  class="form-control option-class select"
                  id="exampleFormControlSelect1"
                >
                  <option value="">---</option>
                  <option
                    class="colour"
                    value="Christianity"
                    id="selectCountry"
                  >
                    Christianity
                  </option>
                  <option class="colour" value="Islam" id="selectCountry">
                    Islam
                  </option>
                </select>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >State Of Origin</label
                >
                <select
                  class="form-control option-class select"
                  v-model="dataObj.profile.state_of_origin"
                  @change="getState()"
                  id="selectState"
                >
                  <option value="">---</option>
                  <option
                    v-for="item in states"
                    :key="item.id"
                    class="colour"
                    :value="item.alias"
                  >
                    {{ item.name }}
                  </option>
                </select>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >L.G.A</label
                >
                <select
                  class="form-control option-class select"
                  id="exampleFormControlSelect1"
                  v-model="dataObj.profile.lga"
                >
                  <option value="">---</option>
                  <option
                    v-for="item of lgas"
                    :key="item.id"
                    class="colour"
                    :value="item.name"
                  >
                    {{ item.name }}
                  </option>
                </select>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">Next of kin name</label>
                <input
                  type="text"
                  class="form-control"
                  placeholder="Enter name of next of kin"
                  v-model="dataObj.profile.next_of_kin"
                />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group mt-2">
                <label for="" class="py-2">Home Address</label>
                <input
                  type="text"
                  class="form-control"
                  placeholder="Enter your home address"
                  v-model="dataObj.profile.address"
                />
              </div>
            </div>
          </div>

          <!-- Work/Bank Details -->
          <h5 class="mt-4 font-weight-bold">Work/Bank Details</h5>
          <div class="row">
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="" class="py-2">Staff ID</label>
                <input
                  type="text"
                  class="form-control"
                  placeholder="Staff id"
                  v-model="dataObj.staff_id"
                  readonly
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >Department</label
                >
                 <input
                v-if="dataObj.department === null "
                  type="text"
                  class="form-control"
                  placeholder="Enter your Department"
                />
                <input
                v-else
                  type="text"
                  class="form-control"
                  placeholder="Department"
                  v-model="dataObj.department.name"
                  readonly
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >Level</label
                >
                <input
                  type="text"
                  class="form-control"
                  placeholder="Level"
                  v-model="dataObj.profile.level"
                  readonly
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2">Role</label>
                <input
                  type="text"
                  class="form-control"
                  placeholder="Role"
                  v-model="dataObj.role.name"
                  readonly
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2"
                  >Date of Appointment</label
                >
                <input
                  type="text"
                  class="form-control"
                  placeholder="Date of Appointment"
                  v-model="dataObj.profile.date_hired"
                  readonly
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="" class="py-2">Account Name</label>
                 <input
                v-if="dataObj.bank_detail === null "
                  type="text"
                  class="form-control"
                  placeholder="Enter your account name"
                />
                <input
                v-else
                  type="text"
                  class="form-control"
                  placeholder="Account Name"
                  v-model="dataObj.bank_detail.account_name"
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="" class="py-2">Account Number</label>
                <input
                v-if="dataObj.bank_detail === null "
                  type="text"
                  class="form-control"
                  placeholder="Enter your account number"
                />
                <input
                v-else
                  type="tel"
                  class="form-control"
                  placeholder="Enter your account number"
                  v-model="dataObj.bank_detail.account_no"
                />
              </div>
            </div>
            <div class="col-md-6">
              <div class="form-group mt-2">
                <label for="exampleFormControlSelect1" class="py-2">Bank</label>
                <select
                v-if="dataObj.bank_detail  === null "
                  class="form-control option-class select"
                  id="exampleFormControlSelect1"
                >
                  <option class="colour" value="" id="selectCountry">
                    ---
                  </option>
                  <option
                    class="colour"
                    v-for="item in banks_list"
                    :key="item.id"
                    :value="item.name"
                  >
                    {{ item.name }}
                  </option>
                </select>
                <select
                v-else
                  class="form-control option-class select"
                  id="exampleFormControlSelect1"
                  v-model="dataObj.bank_detail.bank_name"
                >
                  <option class="colour" value="" id="selectCountry">
                    ---
                  </option>
                  <option
                    class="colour"
                    v-for="item in banks_list"
                    :key="item.id"
                    :value="item.name"
                  >
                    {{ item.name }}
                  </option>
                </select>
              </div>
            </div>
          </div>
          <div class="sign-in-button mt-3">
            <button class="py-3" type="submit" v-if="loading" disabled>
              <div class="d-flex justify-content-center">
                <div class="spinner-border" role="status">
                  <span class="sr-only">Loading...</span>
                </div>
              </div>
            </button>
            <button class="py-3" type="submit" v-else>Submit</button>
          </div>
        </form>
      </div>
    </div>

  <!-- Update Password Modal  -->
    <div class="update_password_container animate__animated animate__fadeIn" v-show="update_password" >
        
        <form action="" class="shadow-lg" >
           <div class="d-flex justify-content-between mb-4 ">
             <h5 class="font-weight-bold ">Update Password</h5>
              <div class="" @click="update_password = !update_password">
                <ion-icon name="close"></ion-icon>
              </div>
              
           </div>
          <div class="mb-3">
            <label for="" class="small">Old Password</label> <br />
            <input type="text" name="" v-model="credentials.old_password" id="" />
            <!-- <p class="small text-danger" v-for="error in errors.email" :key="error.id"> *{{ error }} </p> -->
          </div>
          <div class="mb-3">
            <label for="" class="small">New Password</label> <br />
            <input type="text" name="" v-model="credentials.password" id="" />
            <!-- <p class="small text-danger" v-for="error in errors.email" :key="error.id"> *{{ error }} </p> -->
          </div>
          <div class="mb-4">
            <label for="" class="small">Confirm Password</label> <br />
            <input type="text" name="" v-model="credentials.password_confirmation" id="" />
            <!-- <p class="small text-danger" v-for="error in errors.email" :key="error.id"> *{{ error }} </p> -->
          </div>
          <div>
                <div class="d-flex justify-content-center" v-if="loading">
                    <div class="spinner-border" role="status">
                        <span class="sr-only">Loading...</span>
                    </div>
                </div>
              <button v-else type="submit" class="view-btn small">Update Password</button>
          </div>
        </form>
      </div>
  </div>
</template>


<script>
import helpers from "@/helpers/index.js";
import axios from "axios";
export default {
  data() {
    return {
      loading: false,
      baseUrl: "https://ibomdemo.africanapp.store/",
      states: [],
      selState: "",
      lgas: "",
      roles: "",
      departments: "",
      banks_list: "",
      upload: false,
      update_password: false,
      profile_photo: "",
      credentials: {
        old_password: '',
        password: '',
        confirm_password: '',
      },
      dataObj: {
        first_name: "",
        last_name: "",
        email: "",
        profile: {
          phone_number: "",
          date_of_birth: "",
          gender: "",
          marital_status: "",
          religion: "",
          state_of_origin: "",
          lga: "",
          next_of_kin: "",
          address: "",
        },
        department: {
          name: "",
        },
        role: {
          name: "",
        },
        bank_detail: {
          account_name: "",
          account_no: "",
          bank_name: "",
        },
      },
    };
  },
  methods: {
    getState() {
      var stateOptions = document.getElementById("selectState");
      var selOption = stateOptions.options[stateOptions.selectedIndex].value;
      this.selState = selOption;
      this.getlgas();
    },
    async getStates() {
      let res = await axios.get("https://locus.fkkas.com/api/states");
      this.states = res.data.data;
    },
    async getlgas() {
      let res = await axios.get(
        `https://locus.fkkas.com/api/regions/${this.selState}`
      );
      this.lgas = res.data.data;
    },

    async getUser() {
      let res = await helpers.getUser();
      this.dataObj = res;
      console.log(res);
    },
    async getBanks() {
      let res = await helpers.getBanks();
      this.banks_list = res;
    },
    showPreview($event) {
      var input = event.target;
      this.profile_photo = input.files[0];
      // console.log(this.profile_photo);
      if ($event.target.files.length > 0) {
        var src = URL.createObjectURL(event.target.files[0]);
        var preview = document.getElementById("file-ip-1-preview");
        preview.src = src;
        preview.style.display = "block";
        // var updatePhoto = document.getElementById("update");
        var uploadPhoto = document.getElementById("upload-file");
        // updatePhoto.style.display= "none"
        uploadPhoto.style.display = "block";
      }
    },
    async uploadPhoto() {
      const formData = new FormData();
      //  console.log(this.profile_photo);
      formData.append("file", this.profile_photo);
      try {
        let res = await helpers.updateProfile(formData);
        console.log(res);
        var preview = document.getElementById("file-ip-1-preview");
        preview.style.display = "none";
        // var updatePhoto = document.getElementById("update");
        var uploadPhoto = document.getElementById("upload-file");
        // updatePhoto.style.display= "block"
        uploadPhoto.style.display = "none";
        this.getUser();
        this.$router.go();
      } catch (error) {
        console.log(error);
      }
    },

    async updateProfile() {
      this.loading = true;
      const formData = new FormData();
      formData.append("first_name", this.dataObj.first_name);
      formData.append("last_name", this.dataObj.last_name);
      formData.append("email", this.dataObj.email);
      formData.append("phone_number", this.dataObj.profile.phone_number);
      formData.append("date_of_birth", this.dataObj.profile.date_of_birth);
      formData.append("gender", this.dataObj.profile.gender);
      formData.append("marital_status", this.dataObj.profile.marital_status);
      formData.append("religion", this.dataObj.profile.religion);
      formData.append("state_of_origin", this.dataObj.profile.state_of_origin);
      formData.append("lga", this.dataObj.profile.lga);
      // formData.append("file", this.dataObj.profile.profile_photo);
      formData.append("next_of_kin", this.dataObj.profile.next_of_kin);
      formData.append("address", this.dataObj.profile.address);
      formData.append("account_no", this.dataObj.bank_detail.account_no);
      formData.append("account_name", this.dataObj.bank_detail.account_name);
      formData.append("bank_name", this.dataObj.bank_detail.bank_name);
      try {
        let res = await helpers.updateProfile(formData);
        console.log(res);
        this.getUser();
      } catch (error) {
        console.log(error);
      }
      this.loading = false;
    },
  },
  async created() {
    this.getStates();
    this.getUser();
    this.getBanks();
    console.log(this.dataObj.profile.profile_photo);
  },
};
</script>
