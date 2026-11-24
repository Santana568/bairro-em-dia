# Bairro em Dia — Participação Cidadã para Problemas Urbanos

Plataforma web responsiva para que moradores registrem problemas do bairro (buracos, lixo, iluminação, entre outros), recebam um **protocolo único** e acompanhem a resolução em uma linha do tempo. Desenvolvida com **HTML5 semântico**, **CSS3 (BEM, Flexbox e Grid)** e **JavaScript com módulos ES**, com dados salvos no **Firebase Firestore** e publicada no **Firebase Hosting**.

**Site publicado:** https://bairro-em-dia-ab3f2.firebaseapp.com
**Repositório:** https://github.com/Santana568/bairro-em-dia

---

## Sumário
- [1. Visão Geral do Projeto](#1-visão-geral-do-projeto)
- [2. Estrutura de Diretórios](#2-estrutura-de-diretórios)
- [3. Páginas do Projeto](#3-páginas-do-projeto)
- [4. HTML5 Semântico](#4-html5-semântico)
- [5. Metodologia BEM (Block, Element, Modifier)](#5-metodologia-bem-block-element-modifier)
- [6. Aplicação de Flexbox](#6-aplicação-de-flexbox)
- [7. Aplicação de CSS Grid Layout](#7-aplicação-de-css-grid-layout)
- [8. Responsividade e Media Queries](#8-responsividade-e-media-queries)
- [9. Capturas de Tela](#9-capturas-de-tela)
- [10. Diferenciais Técnicos (Firebase, ViaCEP e Persistência)](#10-diferenciais-técnicos-firebase-viacep-e-persistência)
- [11. Como Executar o Projeto](#11-como-executar-o-projeto)
- [12. Publicação no Firebase Hosting](#12-publicação-no-firebase-hosting)
- [13. Créditos das Imagens](#13-créditos-das-imagens)

---

## 1. Visão Geral do Projeto
Problemas urbanos costumam ficar sem solução por falta de um canal simples e rastreável de comunicação entre moradores e gestão. O **Bairro em Dia** resolve isso permitindo:

- registrar uma ocorrência com foto, descrição e endereço (preenchido automaticamente pelo CEP);
- receber um **protocolo único** no formato `BED-2026-XXXXXX`;
- acompanhar a situação (**Pendente → Em análise → Em andamento → Resolvida**) em uma linha do tempo;
- consultar todas as ocorrências da cidade, com filtros por categoria e situação;
- visualizar indicadores gerais na página inicial.

O projeto é o Trabalho Final (AV2) da disciplina de Programação Web Coding, do curso de Ciência da Computação, e demonstra domínio de estruturação semântica, layouts com Flexbox e Grid, nomenclatura BEM e adaptação a diferentes telas, com integração a um banco de dados em nuvem.

---

## 2. Estrutura de Diretórios
```text
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
```

---

## 3. Páginas do Projeto
O projeto tem **5 páginas HTML interligadas**, com cabeçalho, menu e rodapé consistentes:

1. **`index.html` (Início)**: banner principal, indicadores (registradas, pendentes, em andamento e resolvidas), passo a passo de uso, categorias de problemas e últimas ocorrências.
2. **`registrar.html` (Registrar ocorrência)**: formulário com nome, categoria, título, descrição, CEP, rua, bairro, número, cidade, UF e foto. Ao enviar, exibe o protocolo gerado e lista os protocolos registrados no aparelho.
3. **`ocorrencias.html` (Ocorrências)**: cards com foto, categoria, bairro, data e situação, com filtros por categoria e situação e contador de resultados.
4. **`acompanhar.html` (Acompanhar protocolo)**: busca por protocolo, exibe todos os dados da ocorrência e a linha do tempo da situação.
5. **`sobre.html` (Sobre)**: proposta, benefícios e tecnologias do projeto.

---

## 4. HTML5 Semântico
- **`<header>`**: cabeçalho com logotipo e menu, repetido em todas as páginas.
- **`<nav>`**: menu principal e links do rodapé, com `aria-label`.
- **`<main>`**: conteúdo principal de cada documento.
- **`<section>`**: blocos temáticos (banner, indicadores, como funciona, categorias, últimas ocorrências), ligados aos títulos por `aria-labelledby`.
- **`<article>`**: unidades independentes, como os indicadores e os cards de ocorrência.
- **`<footer>`**: rodapé com navegação e informações do projeto acadêmico.

```html
<section class="banner" aria-labelledby="titulo-banner">...</section>

<article class="indicador indicador--pendentes">
  <span class="indicador__numero" data-pendentes>–</span>
  <span class="indicador__rotulo">Pendentes</span>
</article>
```

---

## 5. Metodologia BEM (Block, Element, Modifier)
As classes seguem a metodologia **BEM**: bloco, elemento (`__`) e modificador (`--`).

### Exemplos reais do projeto
| Tipo | Exemplos |
| :-- | :-- |
| Bloco | `.cabecalho`, `.card`, `.indicador`, `.formulario`, `.linha-tempo`, `.rodape` |
| Elemento | `.card__imagem`, `.card__titulo`, `.card__rodape`, `.cabecalho__menu`, `.formulario__campo`, `.indicador__numero` |
| Modificador | `.cabecalho__link--ativo`, `.indicador--resolvidas`, `.selo--pendente`, `.formulario__entrada--invalida`, `.linha-tempo__item--atual` |

```html
<article class="indicador indicador--registradas">
  <span class="indicador__numero" data-total>–</span>
  <span class="indicador__rotulo">Ocorrências registradas</span>
</article>
```

---

## 6. Aplicação de Flexbox
O Flexbox organiza alinhamento e distribuição unidimensional em vários componentes.

1. **Cabeçalho e menu (`css/style.css`)**: logotipo e links em linha, com quebra quando falta espaço.
   ```css
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
   ```
2. **Cards de ocorrência**: conteúdo em coluna, com o rodapé do card sempre no final.
   ```css
   .card { display: flex; flex-direction: column; }
   .card__conteudo { display: flex; flex-direction: column; gap: .4rem; flex: 1; }
   .card__rodape {
     display: flex;
     flex-wrap: wrap;
     align-items: center;
     justify-content: space-between;
     margin-top: auto;
   }
   ```
3. **Filtros, busca, banner, passos e rodapé**: `.filtros`, `.consulta`, `.banner__acoes`, `.passos`, `.apresentacao` e `.rodape__conteudo` usam `display: flex` com `flex-wrap` e `gap`.

*Propriedades aplicadas:* `display: flex`, `flex-direction`, `justify-content`, `align-items`, `flex-wrap`, `flex` e `gap`.

---

## 7. Aplicação de CSS Grid Layout
O CSS Grid estrutura as grades bidimensionais do projeto.

1. **Painel de indicadores, com áreas nomeadas**:
   ```css
   .painel {
     display: grid;
     gap: 1.25rem;
     grid-template-columns: repeat(4, 1fr);
     grid-template-areas:
       "registradas pendentes andamento resolvidas"
       "referencia referencia referencia referencia";
   }
   ```
2. **Lista de ocorrências e categorias, com colunas adaptáveis**:
   ```css
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
   ```
3. **Formulário de registro em 6 colunas**, para combinar campos de larguras diferentes na mesma linha:
   ```css
   .formulario { display: grid; grid-template-columns: repeat(6, 1fr); gap: 1.1rem; }
   .formulario__campo { grid-column: span 6; }
   ```
4. **Registro e resultado da consulta**, com duas colunas (`.registro` e `.resultado`) e lista de dados em `auto 1fr`.

*Propriedades aplicadas:* `display: grid`, `grid-template-columns`, `grid-template-areas`, `grid-area`, `grid-column`, `gap`, `repeat()`, `minmax()`, `auto-fill` e `auto-fit`.

---

## 8. Responsividade e Media Queries
O layout se adapta a celulares, tablets e computadores com **3 blocos `@media screen`** no final do `css/style.css`:

| Breakpoint | O que muda |
| :-- | :-- |
| `min-width: 769px` | Menu horizontal sempre visível |
| `max-width: 768px` | Menu recolhido com botão, painel em 2 colunas, formulário e resultado em 1 coluna |
| `max-width: 480px` | Tudo em 1 coluna, formulário compacto e botões largos |

```css
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
```

Há também `prefers-reduced-motion`, que desativa transições e animações para quem prefere menos movimento.

---

## 9. Capturas de Tela

### Registro de ocorrência
| Formulário | Protocolo gerado |
| :---: | :---: |
| ![Formulário de registro](img/screenshots/06-registrar-formulario.png) | ![Protocolo gerado após o envio](img/screenshots/01-protocolo-gerado.png) |

### Ocorrências e acompanhamento
| Lista de ocorrências | Acompanhamento por protocolo |
| :---: | :---: |
| ![Lista de ocorrências com filtros](img/screenshots/04-ocorrencias-lista.png) | ![Acompanhar protocolo com linha do tempo](img/screenshots/05-acompanhar-protocolo.png) |

### Linha do tempo e banco de dados
| Consulta de outra ocorrência | Dados no Firestore |
| :---: | :---: |
| ![Consulta de protocolo e linha do tempo](img/screenshots/03-acompanhar-linha-do-tempo.png) | ![Coleção ocorrencias no Firestore](img/screenshots/02-firestore-console.png) |

---

## 10. Diferenciais Técnicos (Firebase, ViaCEP e Persistência)

1. **Firebase Firestore**:
   - Coleção `ocorrencias`, em que cada documento usa o protocolo como ID (`BED-2026-XXXXXX`).
   - Funções em `js/firebase.js`: salvar ocorrência, gerar protocolo único, listar, consultar por protocolo e atualizar a situação.
   - Regras de segurança em `firestore.rules`: leitura pública, criação apenas com situação `pendente`, sem exclusão.
2. **Firebase Hosting**: site publicado com `firebase deploy`.
3. **ViaCEP**: ao digitar o CEP, rua, bairro, cidade e UF são preenchidos automaticamente.
4. **Fotos**: reduzidas no navegador com `canvas` e salvas em JPEG dentro do próprio documento do Firestore, sem uso do Firebase Storage.
5. **Plano B offline**: se o Firestore não responder, a ocorrência é guardada no `localStorage`, recebe protocolo e é enviada ao banco quando a conexão voltar.
6. **Modo gestor (demonstração)**: `ocorrencias.html?gestor=1` permite atualizar a situação. Não há autenticação, então em produção seria necessário adicionar Firebase Authentication e restringir o `update` nas regras.

---

## 11. Como Executar o Projeto

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/Santana568/bairro-em-dia.git
   ```
2. **Acesse a pasta:**
   ```bash
   cd bairro-em-dia
   ```
3. **Abra com um servidor local.** Os scripts usam módulos ES, que não funcionam abrindo o arquivo direto (`file://`). No **VS Code**, use a extensão **Live Server**: clique com o botão direito em `index.html` e escolha *Open with Live Server*.
4. **Configure o Firebase** (para usar o seu próprio projeto):
   1. Crie um projeto em https://console.firebase.google.com.
   2. Em *Build → Firestore Database*, crie o banco de dados.
   3. Em *Configurações do projeto → Seus apps → Web*, registre o app e copie o `firebaseConfig`.
   4. Cole os valores em `js/firebase.js`.
   5. Em *Firestore → Regras*, publique o conteúdo de `firestore.rules`.
5. Abra `ocorrencias.html`: com o banco vazio, aparece o botão **Criar ocorrências de exemplo**.

---

## 12. Publicação no Firebase Hosting

Com a CLI do Firebase (requer Node.js), dentro da pasta do projeto:

```bash
npx firebase-tools login
npx firebase-tools deploy
```

O `firebase.json` publica o site e as regras do Firestore. O `.firebaserc` já aponta para o projeto `bairro-em-dia-ab3f2`. Para publicar só o site, use `npx firebase-tools deploy --only hosting`.

---

## 13. Créditos das Imagens
O banner, as fotos de ruas danificadas e lixo, a imagem do cidadão com o aplicativo e as imagens de painéis são materiais de terceiros, usados com finalidade acadêmica. Os autores e as licenças de cada arquivo devem ser conferidos e listados aqui antes de qualquer uso fora do trabalho.

---

**Autor:** Emanuel Santana ([@Santana568](https://github.com/Santana568))
Programação Web Coding — Ciência da Computação · Trabalho Final (AV2)