
<template>

  <div id="app">
    <div class="leads">
      <Logo />
      <!-- <Logo dark-background /> -->
      <br /><br />
      <h3>
      {{bemvindo}}
      </h3>
       <br />
      <h4>{{empresa}}</h4>
      <br />
      <link href="https://fonts.googleapis.com/icon?family=Material+Icons"
      rel="stylesheet">
      <!-- Bar containing all sort inputs -->
      <div id="sort-bar">
       <input id="search-input" v-model="searchName" type="text"  placeholder=" Procurar lead">
       <input id="search-input" v-model="searchCompany" type="text"  placeholder=" Procurar empresa">
       <input id="search-input" v-model="searchCompanyBs" type="text"  placeholder=" Procurar características">
      </div>

      <!-- Where the array of recipes get rendered as cards -->
      <div id="lead-container">
        <div v-for="lead in filteredLeads" :key="lead.title" class="card">
          <div class="content">
            <h1 class="lead-title">
              {{ lead.name }}
            </h1>
            <p><span class="material-icons">mail</span>
              {{ lead.email }}
            </p>
            <p><span class="material-icons">business</span>
              {{ lead.company.name }}
            </p>
            <p><span class="material-icons">bolt</span>
              {{ lead.company.bs }}
            </p>
             <p><span class="material-icons">phone</span>
              {{ lead.phone }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
     
      searchName: '',
      searchCompany: '',
      searchCompanyBs: '',
      leads: {}, 
      bemvindo: 'Olá, colaborador!',
      empresa: "Nessa tela você pode acessar nossos clientes em potencial. Faça a procura por nome, empresa e ou características da empresa."
    };
  },
  computed: {
    filteredLeads() {
      let filtered = this.leads;

      // Process search input
      if (this.searchName !== '' && this.searchName) {
        filtered = filtered.filter((item) => {
          return item.name
            .toUpperCase()
            .includes(this.searchName.toUpperCase());
        });
      }
      // Process search input
      if (this.searchCompany !== '' && this.searchCompany) {
        filtered = filtered.filter((item) => {
          return item.company.name
            .toUpperCase()
            .includes(this.searchCompany.toUpperCase());
        });
      }
      // Process search input
      if (this.searchCompanyBs !== '' && this.searchCompanyBs) {
        filtered = filtered.filter((item) => {
          return item.company.bs
            .toUpperCase()
            .includes(this.searchCompanyBs.toUpperCase());
        });
      }

      return filtered;
    },
  },
  mounted () {
    axios
      .get('https://jsonplaceholder.typicode.com/users')
      .then(res => {        
        this.leads = res.data;
              })
      
  }
};
</script>


<style lang="scss">
body {
  padding: 20px;
  font-family: Helvetica;
  background: #20262e;
 
}

#app {
  background: #fff;
  transition: all 0.2s;
  border-radius: 4px;
  padding: 20px;
}


h2 {
  font-weight: bold;
  margin-bottom: 15px;
}

h3 {
  font-weight: 600;
  font-size: 16px;
}


@media screen and (max-width: 600px) {
  .lead-container  {
    width: 100%;
    margin-bottom: 20px;
    display: block;
  }
}


.card {
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.3) 0 5px 10px;
  margin: 10px;
 
  padding: 16px;
 
}


div.content {
  padding: 10px;
}


#sort-bar {
  width: 86%;
  margin-left: 10px;
  background-color: #4c57ec;
  display: flex;
  flex-wrap: wrap;
  padding: 15px;
  border-radius: 4px;
  transition: all 0.2s;
}


#search-input {
  margin-right: 10px;  
  border-radius: 5px;
  width: 240px;
  height: 20px;
}


</style>
