<template>
  <div class="row">
    <div class="col-md-6">
      <form>
        <div class="mb-3">
          <label for="ahorro" class="form-label">Ahorro</label>
          <input
            type="number"
            class="form-control"
            id="ahorro"
            min="0"
            v-model="retiro.ahorro"
          />
        </div>
        <div class="mb-3">
          <label for="sueldo" class="form-label">Sueldo</label>
          <input
            type="number"
            class="form-control"
            id="sueldo"
            aria-describedby="sueldoHelp"
            min="0"
            v-model="retiro.sueldo"
          />
          <div id="sueldoHelp" class="form-text">
            Ingrese su sueldo, debe ser un valor positivo.
          </div>
        </div>
        <a
          @click="getRetiro"
          class="btn btn-primary"
          v-on:submit.prevent="onSubmit"
        >
          Realizar retiro
        </a>
      </form>
    </div>
    <div class="col-md-6">
      <div class="h-100 p-5 border rounded-3">
        <h2>Resumen de su retiro</h2>
        <table class="table table-striped">
          <tbody>
            <tr>
              <td style="width: 60%">DXC</td>
              <td class="text-end" id="fila-resultado-dxc">{{ retiro.dxc }}</td>
            </tr>
            <tr>
              <td scope="row" style="width: 60%">Saldo</td>
              <td class="text-end" id="fila-resultado-saldo">
                ${{ retiro.saldo }}
              </td>
            </tr>
            <tr>
              <td scope="row" style="width: 60%">Impuesto</td>
              <td class="text-end" id="fila-resultado-impuesto">
                {{ retiro.impuesto }}
              </td>
            </tr>
            <tr>
              <td scope="row" style="width: 60%">Ahorro</td>
              <td class="text-end" id="fila-resultado-ahorro">
                ${{ retiro.ahorro }}
              </td>
            </tr>
            <tr>
              <td scope="row" style="width: 60%">Sueldo</td>
              <td class="text-end" id="fila-resultado-sueldo">
                ${{ retiro.sueldo }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
//http://localhost:8080/rest/msdxc/dxc?sueldo=10000000&ahorro=250000000

export default {
  name: "App",
  data() {
    return {
      retiro: {
        ahorro: 0,
        sueldo: 0,
        dxc: 0,
        saldo: 0,
        impuesto: 0,
      },
    };
  },
  mounted() {},
  methods: {
    getRetiro() {
      const params = {
        ahorro: this.retiro.ahorro,
        sueldo: this.retiro.sueldo,
      };
      this.axios
        .get("http://127.0.0.1:8090/rest/msdxc/dxc", { params })
        .then((response) => {
          console.log(response.data);
          this.retiro = response.data;
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>
