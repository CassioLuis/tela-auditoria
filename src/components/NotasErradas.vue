<template>
  <div class="border p-1">
    <ul class="cursor-pointer w-full list-none">
      <li
        v-for="({ nome, notas_erradas, open }, index) in erros"
        :key="index"
        class="p-2"
      >
        <span
          class="p-1 rounded select-none hover:bg-gray-500"
          @click="erros[index].open = !erros[index].open"
          >{{ nome }} ({{ notas_erradas.length }})</span
        >
        <table class="li-content" v-if="open">
          <tr>
            <th>Num Doc</th>
            <th>Ser</th>
            <th>Chave</th>
            <th>Emissao</th>
          </tr>
          <tbody
            v-for="{
              num_doc,
              ser,
              chv_nfe,
              dt_doc2,
              id_reg_c100,
              dados_certos,
              dados_errados,
            } in notas_erradas"
            :key="id_reg_c100"
          >
            <tr class="table-view" @click="fold = !fold">
              <td>{{ num_doc }}</td>
              <td>{{ ser }}</td>
              <td>{{ chv_nfe }}</td>
              <td>{{ dt_doc2 }}</td>
            </tr>
            <tr>
              <td class="fold" v-if="fold" colspan="4">
                <div class="flex">
                  <table>
                    <tr>
                      <th colspan="4">Dados Errados</th>
                    </tr>
                    <tr>
                      <th>IE</th>
                      <th>COD MUN</th>
                      <th>COD PART</th>
                      <th>CPF CNPJ</th>
                    </tr>
                    <tr
                      v-for="(
                        { ie, cod_mun, cod_part, cpf_cnpj }, index
                      ) in dados_errados"
                      :key="index"
                    >
                      <td>{{ ie || "Vazio" }}</td>
                      <td>{{ cod_mun || "Vazio" }}</td>
                      <td>{{ cod_part || "Vazio" }}</td>
                      <td>{{ cpf_cnpj || "Vazio" }}</td>
                    </tr>
                  </table>
                  <table>
                    <tr>
                      <th colspan="4">Dados Certos</th>
                    </tr>
                    <tr>
                      <th>IE</th>
                      <th>COD MUN</th>
                      <th>COD PART</th>
                      <th>CPF CNPJ</th>
                    </tr>
                    <tr
                      v-for="(
                        { ie, cod_mun, cod_part, cpf_cnpj }, index
                      ) in dados_certos"
                      :key="index"
                    >
                      <td>{{ ie }}</td>
                      <td>{{ cod_mun }}</td>
                      <td>{{ cod_part }}</td>
                      <td>{{ cpf_cnpj }}</td>
                    </tr>
                  </table>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </li>
    </ul>
  </div>
</template>
<script>
import errosParticipantes from "../../public/errosParticipantes.js";
import errosSerie from "../../public/errosSerie.js";

export default {
  data() {
    return {
      // open: true,
      fold: true,
      erros: [
        {
          nome: "Erros Participantes",
          notas_erradas: errosParticipantes,
          open: false,
        },
        {
          nome: "Erros de Serie",
          notas_erradas: errosSerie,
          open: false,
        },
      ],
    };
  },
  computed: {},
  mounted() {
    // this.showData();
  },
  methods: {
    showData() {
      errosParticipantes.map((item, index) => {
        const arrayDestino = JSON.stringify(this.nota_errada[index]);
        const arrayOrigem = JSON.stringify(item);
        const test = arrayDestino === arrayOrigem;
        test || this.nota_errada.push(item);
      });
    },
    openFold(el) {
      console.log(el.target.nextSibling);
    },
  },
};
</script>
<style scoped>
th,
td {
  border: 1px solid;
  text-align: center;
  padding: 2px;
}
th {
  font-weight: bold;
}
table {
  width: 100%;
}
</style>
