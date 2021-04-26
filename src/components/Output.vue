<template>
  <div>
    <div class="namebox">
      <div class="grid grid-[grid-state]">
        <span>{{ position }}</span>
      </div>
      <div class="line">
        <div
          v-show="selected === 'Mercedes'"
          style="background-color: #00d2be"
        ></div>
        <div
          v-show="selected === 'Red Bull Racing Honda'"
          style="background-color: #0600ef"
        ></div>
        <div
          v-show="selected === 'Mclaren Mercedes'"
          style="background-color: #ff8700"
        ></div>
        <div
          v-show="selected === 'Ferrari'"
          style="background-color: #dc0000"
        ></div>
        <div
          v-show="selected === 'Alpha Tauri Honda'"
          style="background-color: #2b4562"
        ></div>
        <div
          v-show="selected === 'Aston Martin Mercedes'"
          style="background-color: #006f62"
        ></div>
        <div
          v-show="selected === 'Alpine Renault'"
          style="background-color: #0090ff"
        ></div>
        <div
          v-show="selected === 'Alfa Romeo Racing Ferrari'"
          style="background-color: #900000"
        ></div>
        <div
          v-show="selected === 'Williams Mercedes'"
          style="background-color: #005aff"
        ></div>
        <div
          v-show="selected === 'Haas Ferrari'"
          style="background-color: #ffff"
        ></div>
      </div>
      <div class="driver">
        <div class="name">
          <span class="firstname">{{ firstname }}</span
          ><span class="lastname">{{ lastname }}</span>
        </div>
        <div class="constructor">{{ selected }}</div>
      </div>
      <div class="ident">
        <div class="number">{{ number }}</div>
        <div class="abbreviation">{{ short }}</div>
      </div>
    </div>
    <div class="inputBox">
      <select v-model="position">
        <option disabled value="">Position</option>
        <option v-for="index in 20" :key="index">{{ index }}</option>
      </select>

      <input type="text" placeholder="Firstname" v-model="firstname" />
      <input type="text" placeholder="Lastname" v-model="lastname" />
      <input type="text" maxlength="2" placeholder="Number" v-model="number" />
      <input
        type="text"
        :maxlength="max"
        placeholder="Shortname"
        v-model="short"
      />
      <select v-model="selected">
        <option disabled value="">Please select constructor</option>
        <option>Mercedes</option>
        <option>Red Bull Racing Honda</option>
        <option>Mclaren Mercedes</option>
        <option>Ferrari</option>
        <option>Alpha Tauri Honda</option>
        <option>Aston Martin Mercedes</option>
        <option>Alpine Renault</option>
        <option>Alfa Romeo Racing Ferrari</option>
        <option>Williams Mercedes</option>
        <option>Haas Ferrari</option>
      </select>
    </div>
    <div class="times">
      <h2>Season: {{ infos.season }}</h2>
      <h2>Round: {{ infos.round }}</h2>
    </div>

    <table class="standTable">
      <thead>
        <tr>
          <th>Position</th>
          <th>Number</th>
          <th>Driver</th>
          <th>Car</th>
          <th>Nationality</th>
          <th>Points</th>
        </tr>
      </thead>
      <tbody v-for="(info, index) in infos.DriverStandings" :key="index">
        <tr>
          <td>{{ info.position }}</td>
          <td>{{ info.Driver.permanentNumber }}</td>
          <td>{{ info.Driver.givenName }} {{ info.Driver.familyName }}</td>
          <td>{{ info.Constructors[0].name }}</td>
          <td>{{ info.Driver.nationality }}</td>
          <td>{{ info.points }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      position: "",
      firstname: "",
      lastname: "",
      selected: "",
      number: "",
      short: "",
      max: 3,
      infos: [],
    };
  },
  props: ["infos"],

  created() {
    fetch("http://ergast.com/api/f1/current/driverStandings.json")
      .then(res => {
        return res.json();
      })
      .then(res => {
        this.infos = res.MRData.StandingsTable.StandingsLists[0];
      });
  },
};
</script>

<style lang="scss">
@import "../assets/formula1.scss";
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@500&display=swap");

.inputBox {
  border-radius: 5px;
  text-align: center;
  box-sizing: border-box;

  input,
  select {
    align-items: center;
    justify-content: center;
    padding: 12px 20px;
    margin: 8px 2px;
  }
}
.standTable {
  margin-left: auto;
  margin-right: auto;
  border-collapse: collapse;
  font-size: 16px;
  min-width: 400px;

  thead tr {
    color: black;
  }
  th,
  td {
    padding: 6px 15px;
  }
  tbody tr {
    border-bottom: 1px solid #dddd;
  }
}
.times {
  display: flex;
  align-items: center;
  justify-content: center;

  h2 {
    margin-left: 1rem;
  }
}
</style>
