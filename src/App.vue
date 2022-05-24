<template>
  <div id="app">
      <div class="div-principal border" :class="cor"> 
        Cor: {{ cor }}
        <br>
        Posição x do mouse: {{ posicaoX }} 
        <br>
        Posição y do mouse: {{ posicaoY }}
      </div>
      <hr>

      <div @click="mudarCor('verde')" class="div-conteudo border"></div>
      
      <div class="div-conteudo border" 
          @mouseover="mudarCor('azul')" 
          @mouseout="mudarCor('vermelho')">
      </div>

      <div class="div-conteudo border" @mousemove="mudarCor('roxo')" @mouseout="mudarCor('branco')"> </div>

      <div class="div-conteudo border" @mousemove="coordenadas($event)"></div>
      <hr>

      <a href="https://google.com.br" target="_blank"
        v-on:click="prevenirComportamentoPadrão()">
        LINK
      </a>
      <br>
      Mensagem: {{ msg }}

      <hr>
      <a href="https://google.com.br" target="_blank"
          v-on:click.prevent="prevenirComportamentoPadrão()">
          LINK
      </a>
      <br>
      Mensagem: {{ msg }}

      <hr>
      <button @click.once="executarUmaVez()">
        Botão
      </button>
      <p>Cliques: {{ cliques }}</p>   

      <hr>
      <form @submit.prevent.once="previnirUmaVez()">
        <button type="submit"> Enviar </button>
      </form>
      <p>Formulário: {{ formulario }}</p>

      <hr>
      <input type="text" @keyup="capturandoTeclas($event)">
      <p>Teclas : {{ teclas }}</p>
      
      <br>
      <input type="text" @keyup.x="capturandoTeclas($event)">
      <p>Teclas : {{ teclas }}</p>

      <br>
      <input type="text" @keyup.Shift.Enter="capturandoTeclas($event)">
      <p>Teclas : {{ teclas }}</p>

      <hr>
      <input type="text" id="inputTexto">
      <button @click="selecionarElementoFilho()">Botão 2</button>
      <br>
      <button @click="selecionarElementoEAPropriedadeFilho()">Botão 3</button>
      <br>
      <button @click="selecionarElementoERecuperValorDaPropriedadeFilho()">Botão 4</button>
      <p>Nome Recuperado: {{ nomeRecuperado }}</p>

      <hr>
      <select id="opcoes">
          <option value="A">Opção 1</option>
          <option value="B">Opção 2</option>
          <option value="C">Opção 3</option>
      </select>
      <button @click="selecionarOpcao()">Botao 5</button>

      <hr>
      <div id="bloco">Conteudo dentro da tag</div>
      <button @click="recuperarConteudoTag()">Botao 6</button>

      <hr>
      <!-- V-if simples -->
                        <!--Função toggle-> quando clico passa a valer true e se clicar
                         novamente ele passa a valer false.
                         para isso usamos (!)NOT
                        -->    
      <button @click="exibirSaldo = !exibirSaldo">.
        <span v-if="!exibirSaldo" > Saldo Exibido </span>
        <span v-if="exibirSaldo = false"> Ocutar saldo </span>  
       </button>
      <p>Saldo: <span v-if="exibirSaldo">R$ {{ saldo }} </span></p>

      <hr>

      <!-- V-if e v-else -->
      Idade: <input type="text" id="idade" @blur="setIdade()">
      <p v-if="idade < 18"> Menor de Idade</p>
      <p v-else>Maior de Idade</p>
      {{ idade }}

       <hr>

      <!-- V-if , v-else-if e v-else  -->
      Nota: <input type="text" id="inputNota" @blur="setNota()">
      <p v-if="nota == ''"> Digite a nota do Aluno </p>
      <p v-else-if="nota >= 7 && nota <= 10"> Aluno Aprovado </p>
      <p v-else-if="nota >= 5 && nota < 7"> Aluno está em recuperação </p>
      <p v-else-if="nota < 0 && nota > 10"> A nota informada não é válida </p>
      <p v-else> Aluno reprovado </p>
    
    <hr>

    <!--V- show-->
    <p @mouseover="textoAjuda = true" @mouseout="textoAjuda = false">Emxemplo tootip</p>
    <div v-show="textoAjuda">
      <h3>Texto ajuda </h3>
      <p> conteudo Texto ajuda</p>
    </div>

      <hr>
      <!--Adicionando elemetos HTML do data para o HTML principal.-->
      <div v-html="elementoHTML"></div>

  <hr>
    <!-- V-once -> Renderiza o elemento HTML somente uma vez.-->
    <p v-once> Saldo Inicial: {{ saldoConta }}</p>
    <p> Saldo atualizado: {{ saldoConta }}</p>
    <input type="text" id="valorSaldo">
    <button @click="creditar()"> Creditar </button>
    <button @click="debitar()"> Debitar </button>

    <hr>
      <!--V-for-> Trabalhando com laço de repetição.-->
      <ul>
        <li v-for="curso in cursos" :key="curso.id"> {{ cursos }} </li>
      </ul>

      <!--Posso fazer tambem dessa firma para recuperar as variáveis.-->
      <ul>
        <li v-for="curso in cursos" :key="curso.id" v-text="cursos"></li>
      </ul>

       <!--Recuperar o key do array-->
      <ul>
        <li v-for="(curso, key) in cursos" 
        :key="curso.id">{{ key }} - {{ cursos }}</li>
      </ul>

      <!--Posso usar dessa forma-->
      <ul>
        <li v-for="(curso, key) in cursos" 
        :key="curso.id" v-text="key +' - ' + cursos"></li>
      </ul>

      <hr>

      <!--V-for-> Interação sobre objetos -->
      <table border="2px"> 
        <thead>
          <tr>
            <th>ID</th>
            <th>Titulo</th>
            <th>Descricao</th>
          </tr>
        </thead>
        <tbody>
            <tr v-for="(curso, index) in cursos2" :key="curso.id">
            <td> {{ index }} </td>
            <td> {{ curso.titulo }}</td>
            <td> {{ curso.descricao }}</td>
          </tr>
        </tbody>
      </table>

      <!--Destructor do JS-->
      <table border="2px"> 
        <thead>
          <tr>
            <th>ID</th>
            <th>Titulo</th>
            <th>Descricao</th>
          </tr>
        </thead>
        <tbody>
            <tr v-for="({titulo, descricao}, index) in cursos2" :key="index">
            <td> {{ index }} </td>
            <td> {{ titulo }}</td>
            <td> {{ descricao }}</td>
          </tr>
        </tbody>
      </table>

      <hr>
      <!-- Adicionando e removendo elementos no V-for-->

      <ul>
        <li v-for="c in comentarios" :key="c.id"></li>
      </ul>
      <button @click="adicionarComentario()"> Adicionar </button>
      <button @click="removerComentario()"> Remover </button>
      <button @click="atualizarComentario()"> Atualizar </button>

      <hr>

      <!-- Propiedade Computada(Computed)-->
      <h4>Adicionar pacientes</h4>
      <span>Nome:</span><input type="text" id="inputNome">
      <span>Idade:</span><input type="text" id="inputIdade">
      <span>Plano:</span><input type="text" id="inputPlano">
      <button @click="adicionarPaciente()"> Adicionar </button>

      <h4>Pacientes Cadastrados</h4>
      <p v-for="p in pacientes" :key="p.id"> {{ p.nome }} </p>

      <h4>último paciente Cadastrado</h4>
      <p v-if="pacientes.length > 0">
        {{ utimoPaciente }}
      </p>

      <h4>Paciente do plano OURO</h4>
      <p v-for="p in planoOuro" :key="p.id"> {{ p.nome }} </p>

      <hr>
      <!-- V-model -->
      <!-- Passando o valor do atributo Vue para o Template.-->
        <input type="text" :value="jogador">

      <!--Passando o valor do template para o atrivuto Vue-->
         <input type="text" :value="jogadorReserva" @keyup="setJogadorReserva($event)">
         <!--Posso fazer dessa forma também(Sem criar um método específico)-->
          <input type="text" :value="jogadorReserva" @keyup="jogadorReserva = $event.target.value">
      
      <!-- Ao invez de utilizar os exemplo acima podemos resolver tudo com o V-Model-->
      <!--Exemplo com o V-Model(dataBind de mão dupla)-->
      <input type="text" v-model="goleiro">

      <hr>
      <!-- Exercitando V-Model com atributos de entrada de dados do template.-->

      <!--Input do tipo Radio-->
      <input type="radio" value="A" v-model="apto"> Apto ao Jogo
      <input type="radio" value="N" v-model="apto"> Não está Apto ao Jogo
      <br>
      jogador está apto: {{ apto }}

      <!--Input do tipo Select-->
      <select v-model="contratacao">
        <!--Field disable e padrão da documentação-->
        <option value="" disabled> Selecionar uma Opção </option>
        <option value="1">Em Negociação</option>
        <option value="1">Em Negociação</option>
        <option value="2">Contrato Enviado</option>
        <option value="3">Contrato Assinado</option>
      </select>
      <br>
      Verificador de status para contratação: {{ contratacao }}

      <!--Input do tipo checkbox-->
      <input type="checkbox" value="1" v-model="salario">Pago
      <input type="checkbox" value="2" v-model="salario">Aguardando autorização
      <input type="checkbox" value="3" v-model="salario">Pagamento não efetuado
      <br>
      Pagamento: {{ salario }}

      <!--Input do tipo TextArea-->
      <textarea v-model="descricaoContratacao"></textarea>
      <br>
      Descrição: {{ descricaoContratacao }}

      <!--Busca por nome usando o atributo watch-->
      <span>Nome: </span> <input type="text" v-model="nomePesquisado">
      <br>
      <ul>
        <li v-for="n in list" :key="n.id">{{ n.nome }}</li>
      </ul>

  </div>
</template>

<script>


export default{

  data() {
    return {
      cor: 'branco',
      posicaoX: 0,
      posicaoY: 0,
      msg: '',
      cliques: 0,
      formulario: '',
      teclas: '',
      nomeRecuperado: '',
      saldo: 4500.00,
      exibirSaldo: false,
      idade: 0,
      nota: 0,
      textoAjuda: false,
      elementoHTML: '<p><b>Site</b></p><a href="http.google.com.br">Google</a>',
      saldoConta: 1100,
      cursos: ['Laravel' , 'Java' , 'Angular', 'Javascript'],
      cursos2: {
        1000: { titulo: 'Laravel', descricao: 'Domine o framework PHP.' },
        1001: { titulo: 'Java', descricao: 'Aprenda Java' }
      },
      comentarios: [
        {id: 1, cometario: 'Comentario 1'},
        {id: 2, cometario: 'Comentario 2'},
        {id: 3, cometario: 'Comentario 3'}
      ],
      pacientes: [],
      jogador: 'Ronaldo',
      jogadorReserva: '',
      goleiro: '',
      apto: '',
      contratacao: '',
      salario: [],
      descricaoContratacao: '',
      nomePesquisado: '',
      pesquisaPorNomes: [
        {nome: 'Junior', idade: 32},
        {nome: 'Arnaldo', idade: 20},
        {nome: 'Pedro', idade: 68},
        {nome: 'Gustavo', idade: 66},
        {nome: 'Fernando', idade: 71},
      ],
      list: []
    }  
  },
  methods: {
    mudarCor(c){
      this.cor = c
    },
    coordenadas(e){
      this.posicaoX = e.clientX;
      this.posicaoY = e.clientY;
    },
    prevenirComportamentoPadrão(){
      this.msg = 'Comportamento padrão ativado'
    },
    executarUmaVez(){
      this.cliques ++;
    },
    previnirUmaVez(){
      this.formulario = 'Previnindo o comportamento padão.'
    },
    capturandoTeclas(e){
      this.teclas += e.key;
    },
    selecionarElementoFilho(){
      console.log(inputTexto);
    },
    selecionarElementoEAPropriedadeFilho(){
      console.log(inputTexto.type);
    },
    selecionarElementoERecuperValorDaPropriedadeFilho(){
      this.nomeRecuperado = inputTexto.value;
      console.log(this.nomeRecuperado);
    },
    selecionarOpcao(){
      console.log(opcoes.value)
    },
    recuperarConteudoTag(){
      console.log(bloco.innerHTML);
    },
    setIdade(){
      this.idade = idade.value;
    },
    setNota(){
      this.nota = inputNota.valeu;
    },
    creditar(){
      this.saldoConta += parseFloat( valorSaldo.value );
    },
    debitar(){
      this.saldoConta -= parseFloat( valorSaldo.value );
    },
    adicionarComentario(){
      this.comentarios.push({id: 3, cometario: 'Comentário 3'});
    },
    removerComentario(){
      this.comentarios.pop();
    },
    atualizarComentario(){
      this.$set(this.comentarios, 1 , 'Novo Comentário');
    },
    adicionarPaciente(){
      this.pacientes.push({
        nome:inputNome.valeu,
        idade: inputIdade.valeu,
        plano: inputPlano.valeu
      });
    },
    setJogadorReserva(e){
      this.jogadorReserva = e.target.valeu;
    }
  },
  computed: {
    utimoPaciente(){
        let key = this.pacientes.length - 1
        let txt = ''
        txt += 'Paciente: ' + this.pacientes[key].nome
        txt += ', Idade: ' + this.pacientes[key].idade
        txt += ', Plano: ' + this.pacientes[key].plano

        return txt;
    },
    planoOuro(){
      return this.pacientes.filter(e => e.plano === 'Ouro');
    }
  },
  watch: {
    //Observando a mudança de estado do atributo pequisa por nome.
    //Temos que ter o mesmo nome do atributo para o método.
    //Opcionalmente podemos pegar o InputNovo e o inputAntigo como parâmetro dos métodos.
    nomePesquisado(inputNovo){
      this.list = this.pesquisaPorNomes.filter(n => n.nome.match(inputNovo));
    }
  }
}
 
</script>

<style>

  .div-principal{
    width: 200px;
    height: 400px ;
  }

  .border{
    border: 2px solid;
  }

  .div-conteudo{
    width: 50px;
    height: 20px;
    display: inline-block;
  }

  .verde{
    background-color: green;
  }

  .azul{
    background-color: blue;
    color: white;
  }

  .branco{
    background-color: white;
  }

  .vermelho{
    background-color: red;
    color: black;
  }
  
  .roxo{
    background-color: purple;
    color: bisque;
  }

</style>
