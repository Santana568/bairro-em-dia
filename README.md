Bairro em Dia — Participação Cidadã para Inquéritos Urbanos

Plataforma web responsiva para que moradores registrem problemas do bairro (buracos, iluminação,, entre), protocolo únicoosterem um protocolo único e resolução a em uma linha do tempo. Desenvolvida com HTML5 semântico, CSS3 (BEM, Flexbox e Grid) e JavaScript com módulos ES, com dados salvas no Firebase Firestore e publicado no Firebase Hosting.

Site publicado: https://bairro-em-dia-ab3f2.firebaseapp.com Repositório: https://github.com/Santana568/bairro-em-dia
Sumário

    1. 1. Visão Geral do Projeto
    2. 2. Estrutura de Diretórios
    3. Páginas do Projeto
    4. 4. HTML5 Semântico
    5. Metodologia BEM (Bloco, Elemento, Modificador)
    6. Aplicação de Flexbox
    7. Aplicação de CSS Grid Layout
    8. Responsividade e Consultas de Mídia
    9. Capturas de Tela
    10. Diferenciais Técnicos (Firebase, ViaCEP e Persistência)
    11. Como Executar o Projeto
    12. Publicação no Firebase Hosting
    13. Créditos das Imagens

1. 1. Visão Geral do Projeto

Problemasssários urbanos sem sem por falta de falta de um canal simples e rastreável de comunicação entre e gestão. O Bairro em Dia resolver istônimo:

    registrador uma ocorrência com foto, e endereço (preenchido automaticamente pelo CEP);
    Receber um protocolo único no formato BED-2026-XXXXXX;
    a (Pendente → Em → Em andamento → situação Resolvida) em uma linha do tempo;
    todas como ocorrências da cidade, com consultar filtros por categoria e;
    Visual images gerais na inicial.

O projeto é o Trabalho Final (AV2) da disciplina de Programação Web Codificação, do curso de Ciência da Computação, e demonstração domínio de estruturação semântica, layouts com Flexbox e Grid, nomenclatura BEM adaptação a diferentes telas, com um banco de dados em nuvem.
2. 2. Estrutura de Diretórios

bairro-em-dia/
├── css/
│   └── style.css            # Estilos globais, componentes BEM, layouts e media queries
├── js/
│   ├── main.js              # Menu responsivo e aviso de configuração do Firebase
│   ├── firebase.js          # Conexão com o Firestore, protocolo, listagem e atualização
│   ├── formularios.js       # Registro e acompanhamento: validação, CEP, foto e protocolo
│   └── ocorrencias.js       # Listagem, filtros, detalhes e atualização de situação
├── images/
│   ├── banner/              # Imagem do banner principal
│   ├── ocorrencias/         # Fotos de problemas urbanos
│   ├── plataforma/          # Imagens da plataforma em uso
│   └── dashboards/          # Imagens de painéis de indicadores
├── img/
│   └── screenshots/         # Capturas de tela usadas neste README
├── index.html               # Início: banner, indicadores, como funciona e categorias
├── registrar.html           # Formulário de registro de ocorrência
├── ocorrencias.html         # Lista de ocorrências com filtros
├── acompanhar.html          # Consulta por protocolo e linha do tempo
├── sobre.html               # Apresentação do projeto
├── firestore.rules          # Regras de segurança do Firestore
├── firebase.json            # Configuração do Hosting e das regras
├── .firebaserc              # Projeto Firebase associado
└── README.md                # Documentação técnica

3. Páginas do Projeto

O projeto páginas tem 5 HTML interligadas, com cabeçalho, menu e rodapés consistente:

    index.html(Início): banner principal, indicadores (registradas, pendentes, em e resoldados e resolvidas), passo a passo de uso, de problemas e últimas oportunidades.
    registrar.html(Registrador ocorrência): formulário com nome, categoria título, descrição, CEP, rua, bairro de número, cidade, UF e foto. Ao enviar, o protocolo de gênero e lista os protocolos registrados no aparelhos.
    ocorrencias.html(Os): cards com foto, categoria, bairro, data e, com filtros por categoria e situação e contador de resultados.
    acompanhar.html(Acompanhar protocolo): busca por protocolo, atéondes de dados os dados da e a linha do tempo da situação da.
    sobre.html(Sobre): proposta, benefícios e tecnologias do projeto.

4. 4. HTML5 Semântico

    <header>: cabeçalho com logotipo e menu, repetido em todas como páginas.
    <nav>: menu principal e links do rodapé, com aria-label.
    <main>: conteúdo principal de cada documento.
    <section>: blocos temtemáticos (banner,, indicadores como categorias, categorias, últimas), títulos aso por aria-labelledby.
    <article>: unidades independentes, como os indicadores e os cartões de ocorrência.
    <footer>: rodapé com navegação e do projeto de informação acadêmico.

<section class="banner" aria-labelledby="titulo-banner">...</section>

<article class="indicador indicador--pendentes">
  <span class="indicador__numero" data-pendentes>–</span>
  <span class="indicador__rotulo">Pendentes</span>
</article>

5. Metodologia BEM (Bloco, Elemento, Modificador)

Como classes metodologia a siga BEM : bloco, elemento (__) edmodificador (--).
Exemplos reais do projeto
Tipo 	Categoria: Exemplos
Bloco 	.cabecalho, .card, .indicador, .formulario, .linha-tempo, .rodape
Elemento 	.card__imagem, .card__titulo, .card__rodape, .cabecalho__menu, .formulario__campo, .indicador__numero
Modificador 	.cabecalho__link--ativo, .indicador--resolvidas, .selo--pendente, .formulario__entrada--invalida, .linha-tempo__item--atual

<article class="indicador indicador--registradas">
  <span class="indicador__numero" data-total>–</span>
  <span class="indicador__rotulo">Ocorrências registradas</span>
</article>

6. Aplicação de Flexbox

O Flexbox alinhamento organizado e unidimensional em componentes de distribuição.

    Cabeçalho e menu (css/style.css): logotipo e links em linha, quebra com quano falta espaço.

    .cabecalho__conteudo {
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 1rem;
    }
    .cabecalho__menu {
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      gap: .25rem;
    }

    Cartões de ocorrência: conteúdo em, coluna o rodapé do cartão sem última série.

    .card { display: flex; flex-direction: column; }
    .card__conteudo { display: flex; flex-direction: column; gap: .4rem; flex: 1; }
    .card__rodape {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      margin-top: auto;
    }

    Filtros, busca, banner, passos e rodapé : .filtros, .consulta, .banner__acoes, .passos, .apresentacaoe .rodape__conteudouso display: flexcom flex-wrape gap.

Propriedades aplicadas: display: flex, flex-direction, justify-content, align-items, flex-wrap, flexe gap.
7. Aplicação de CSS Grid Layout

O CSS Grid estrutura como graus bidimensionais do projeto.

    Indicadores de painel de, com áreas nomeadas:

    .painel {
      display: grid;
      gap: 1.25rem;
      grid-template-columns: repeat(4, 1fr);
      grid-template-areas:
        "registradas pendentes andamento resolvidas"
        "referencia referencia referencia referencia";
    }

    Lista de ocorrências e categorias, com colunas adaptáveis:

    .ocorrencias {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(min(100%, 300px), 1fr));
      gap: 1.5rem;
    }
    .categorias {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(100%, 210px), 1fr));
      gap: 1.25rem;
    }

    Formulário de registro em 6 colunas, para campos combinar desempreendedora diferente nalinha:

    .formulario { display: grid; grid-template-columns: repeat(6, 1fr); gap: 1.1rem; }
    .formulario__campo { grid-column: span 6; }

    Registro e resultado da consulta, com duas colunas ( .registroe .resultado) e lista de dados de em auto 1fr.

Propriedades aplicadas: display: grid, grid-template-columns, grid-template-areas, grid-area, grid-column, gap, repeat(), minmax(), auto-fille auto-fit.
8. Responsividade e Consultas de Mídia

O layout se adapta a, celulares tablets e computadores com 3 blocos nenhum do final fazer css/style.css:
Ponto de ruptura 	O que muda
min-width: 769px 	Menu horizontal sempre
max-width: 768px 	Menu recolhido com botão, painel em 2 colunas, e formulário em 1 resultado coluna
max-width: 480px 	Tudo em 1, formulário de botões de coluna e largos

@media screen and (max-width: 768px) {
  .painel {
    grid-template-columns: repeat(2, 1fr);
    grid-template-areas:
      "registradas pendentes"
      "andamento resolvidas"
      "referencia referencia";
  }
  .registro  { grid-template-columns: 1fr; }
  .resultado { grid-template-columns: 1fr; }
}

Categoria: Há também prefers-reduced-motion, que desativa transições e animações para quem prefere mensa.
9. Capturas de Tela
Registro de ocorrência
Formulário 	Protocolo de Geradores
Formulário de registro 	Protocolo de Geradores de Envios pó
Os e
Lista de ocorrências 	Acompanhamento por protocolo
Lista de ocorrências com filtros 	Acompanhador protocolo com linha do tempo
Linha do tempo e banco de dados
Consulta de outra ocorrência 	Dados no Firestore
Consulta de protocolo e linha do tempo 	Coleção ocicâncias no Firestore
10. Diferenciais Técnicos (Firebase, ViaCEP e Persistência)

    Firebase Firestore:
        Coleção ocorrencias, em que document cada usa o protocolo como ID (BED-2026-XXXXXX).
        Categoria: Funções em js/firebase.js:varvar ocorrência, gerar protocolo único, senhor, consulte por lista de protocolo e atual.
        Regras de segurança em firestore.rules: leitura pública, criação apenas com pendente, sem.
    Firebase Hosting : site publicado em firebase deploy.
    ViaCEP : ao digitalar o CEP, rua, bairro, cidade e UF são preenchidos automaticamente.
    Fotos :s no browser com canvase salvas em JPEG próprio do do documento Firestore, sem uso do Firebase Storage.
    Plano B offline : se o Firestore não responder, a é guardada no localStorage, recebe protocolo e enviado é ao banco quando a volta ligação.
    Mododo (demonstração): ocorrencias.html?gestor=1permite a. Não há autenticação, em em produção de adnorias de desenvolvimento de Firebase Autenticação e de restritor updatenas regras.

11. Como Executar o Projeto

    Clone o:

    git clone https://github.com/Santana568/bairro-em-dia.git

    Assuma um macarrão:

    cd bairro-em-dia

    Abra com um servidor local. Os scripts usa módulos ES, que não o arquivo direto anábola (file://). No VS Code, use um Live Server : clique com direito botão em extensão index.htmle escolha Abrir com o Live Server.
    Configurar o Firebase (para uso do seu projeto):
        Crie um projeto em https://console.firebase.google.com.
        Em Build → Firestore Database, cry o banco de dados.
        Em Doncos do projeto → Seus apps → Web, registre o app e cópia o firebaseConfig.
        Cole valores os em js/firebase.js.
        Em Firestore → Regras, publique o conteúdo de firestore.rules.
    Abra ocorrencias.html: com o banco aparecem, vazio o Criar ocorrências de botão.

12. Publicação no Firebase Hosting

Com a CLI do Firebase (requer Node.js), da pasta do interior do projeto:

npx firebase-tools login
npx firebase-tools deploy

O firebase.jsonpublica o site e como regras do Firestore. O .firebasercapontar já já projeto bairro-em-dia-ab3f2. Para publicação o site, use só npx firebase-tools deploy --only hosting.
13. Créditos das Imagens

O banner, como listras de ruas de danásias e, imagem do cidadão com o appagrama imagens e como de de painéis são instalações de acadêmica, com tamanhos de tabuleiro, com. Os autores e licenças como cada de arquivo dem servo conferem e aqui listados antes de qualquer trabalho para uso.

Autor: Emanuel Santana (@Santana568@Santana568) Programação Web Coding — Ciência da Computação · Trabalho Final (AV2)
