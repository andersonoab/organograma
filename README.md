# Organograma ADP Sonova (HTML + Excel/CSV + OneDrive)

Este projeto é um Organograma interativo em HTML, totalmente executável no navegador, que permite carregar uma base de colaboradores (Excel ou CSV), agrupar por Área (Diretoria), e montar automaticamente a hierarquia por Gestor x Subordinados.

O arquivo é 100% front-end (sem backend), e funciona por:
- Upload local de Excel/CSV
- Link OneDrive/SharePoint (quando for link de download direto)
- Persistência automática no localStorage (memória do navegador)

---

## Arquivos do projeto

- `index.html`
  - Arquivo único contendo:
    - HTML
    - CSS
    - JavaScript
    - Leitura de Excel/CSV via SheetJS
    - Persistência via localStorage
    - Controles de busca, navegação e expansão

---

## Principais funcionalidades

### 1) Carregar dados (Excel/CSV)
Você pode carregar a base de duas formas:

1. Upload local:
   - Clique em "Escolher arquivo"
   - Aceita `.xlsx`, `.xls`, `.csv`

2. Link OneDrive/SharePoint:
   - Cole o link no campo
   - Clique em "Carregar do OneDrive"

O sistema tenta automaticamente:
- Detectar se o arquivo é CSV ou Excel
- Gerar variações de link com `download=1`
- Ler CSV mesmo quando o link for do Google Sheets

---

### 2) Agrupamento por Área
O agrupamento principal é feito usando a coluna:

- `2-Diretoria`

Caso não exista valor, o colaborador cai em:
- `Sem Área`

---

### 3) Hierarquia por Gestor
A relação Gestor x Subordinado é feita usando:

- `38-Matrícula Gestor` (matrícula do gestor)
- `9-Matricula` (matrícula do colaborador)

O organograma monta os filhos automaticamente, desde que:
- A matrícula do gestor exista dentro da mesma Área.

---

### 4) Expandir / Colapsar níveis
O organograma possui 3 formas de navegação:

- Botão `+ / -` no lado esquerdo do gestor
- Clique na caixa do gestor (nome/cargo) abre e fecha o nível
- Botões globais:
  - `Fechar Todos (Visão Total)`
  - `Abrir Todos (Todos os níveis)`

---

### 5) Busca por nome ou função
O campo de busca permite localizar colaboradores por:

- Nome
- Cargo/Função

Comportamento:
- Marca todas as ocorrências em amarelo
- A ocorrência ativa fica destacada
- Botão "Próximo" navega entre os resultados
- Tecla Enter:
  - Se já houver resultados, vai para o próximo
  - Se não houver resultados, executa a busca

---

### 6) Navegação rápida (Áreas e Gestores)
O sistema gera automaticamente 2 menus:

- Áreas
- Gestores (somente quem possui subordinados)

Ao clicar no gestor, a página rola até ele.

---

### 7) Memória automática (localStorage)
Após carregar um arquivo, o sistema salva automaticamente:

- O dataset já estruturado (hierarquia pronta)
- A última URL usada
- A última fonte

Assim, ao abrir o `index.html` novamente, ele tenta restaurar automaticamente a última base.

Botão disponível:
- `Limpar memória`

---

## Estrutura mínima esperada da base

Para funcionar corretamente, a base deve conter as colunas abaixo (mesmo nome):

- `2-Diretoria`
- `9-Matricula`
- `10-Nome`
- `29-Título Cargo`
- `38-Matrícula Gestor`
- `39-Gestor `

Observação importante:
- A coluna `39-Gestor ` possui um espaço no final (isso está mantido como está no arquivo original).

---

## Como executar

### Opção 1 (mais simples)
1. Baixe o arquivo `index.html`
2. Dê duplo clique
3. Ele abrirá no navegador
4. Carregue um Excel ou CSV

---

## Publicar no GitHub Pages
1. Crie um repositório no GitHub
2. Suba o arquivo `index.html`
3. Vá em:
   - Settings > Pages
4. Escolha:
   - Branch: `main`
   - Folder: `/root`
5. Salve

O GitHub vai gerar uma URL pública.

---

## Observações importantes (OneDrive/SharePoint)
O navegador só consegue carregar arquivos por link se:
- O link for público, ou
- For um link direto de download do arquivo

Se o link abrir uma tela de login/preview do SharePoint, o projeto não consegue ler o arquivo por segurança do navegador.

Solução nesses casos:
- Baixar o arquivo e carregar localmente
- Gerar link direto do CSV

---

## Tecnologias usadas

- HTML + CSS + JavaScript puro
- SheetJS (XLSX) via CDN
- localStorage (persistência no navegador)

---

## Histórico de melhorias implementadas

- Botão "Abrir Todos (Todos os níveis)"
- Clique no gestor expandindo/colapsando o nível
- Busca com destaque de termo
- Dropdowns automáticos de Áreas e Gestores
- Persistência completa via localStorage
- Suporte a:
  - Excel local
  - CSV local
  - Link OneDrive/SharePoint
  - Link Google Sheets (export CSV/XLSX)

---

## Autor / Uso interno

Este arquivo foi desenhado para uso operacional em RH / DP, com foco em:
- Organograma de gestores
- Visualização de estrutura de time
- Navegação rápida por diretoria e liderança
- Uso em auditorias e análises de estrutura

Projeto desenvolvido no contexto Sonova / RH Brasil.
