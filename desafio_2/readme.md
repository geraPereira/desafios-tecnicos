# Desafio 2 — Produzindo código com IA generativa (somente **prompts**)


## 🧭 Como usar estes prompts
1. Abra sua IA generativa favorita (ChatGPT/Copilot).  
2. Cole o **Prompt Base** primeiro para dar contexto e regras.  
3. Em seguida, execute **um prompt por funcionalidade** (itens 1–4).  
4. Use os **prompts de validação e refinamento** ao final para ajustar, testar e documentar.

> Dica: quando pedir código à IA, peça **blocos completos**, com **caminhos de arquivos** e **comandos** para rodar e validar.

---

## 🔰 Prompt Base (contexto + regras)
```
Você é um(a) engenheiro(a) sênior em Python/Flask. Vou colar trechos do meu projeto quando necessário.
Quero que você gere código pronto para copiar e colar, com explicações sucintas.

Regras:
- Use Flask (Python 3.10+). Não altere o que já funciona sem necessidade.
- Sempre informe os arquivos a criar/editar com seus caminhos (ex: flask_app/templates/editorias.html).
- Inclua dependências novas em um requirements.txt se forem necessárias.
- Retorne também instruções de execução e verificação (curl/navegador).
- Escreva mensagens de commit Git curtas e objetivas para cada mudança.
- Foque em segurança, tratativas de erro e compatibilidade cross-platform.
- Evite soluções pesadas e mantenha a estrutura simples (templates + static quando houver JS/CSS).
```

---

## 1) Página **`/editorias`** exibindo o CSV `editorias.csv`
**Prompt funcional:**
```
Crie uma rota Flask GET `/editorias` que:
- Leia o arquivo CSV chamado `editorias.csv` localizado na raiz do repositório ou na pasta do app (ajuste o caminho relativo com pathlib).
- Faça a leitura com pandas; se não houver pandas, explique como instalar e forneça alternativa com csv do Python.
- Renderize uma tabela HTML responsiva com Bootstrap (thead/tbody). Se o CSV tiver acentos, garanta encoding UTF-8 e trate exceções.
- Coloque o HTML em `flask_app/templates/editorias.html`. Separe estilo leve em `flask_app/static/editorias.css` se necessário.
- Adicione testes manuais (curl e navegador) e uma breve seção “Como verificar”.
- Não quebre o endpoint `/` existente.

Também:
- Liste as novas dependências no requirements.txt (ex: pandas opcional) e dê o comando de instalação (pip).
- Dê uma mensagem de commit Git para essa mudança.
```

**Dificuldades a considerar:** caminhos relativos do CSV; encoding (UTF-8 vs Latin-1); tabelas grandes (paginação/opcional).

---

## 2) Página **`/catfact`** consumindo a API pública
**Prompt funcional:**
```
Implemente uma rota Flask GET `/catfact` que:
- Faça uma requisição GET a https://catfact.ninja/fact usando `requests` com timeout e tratativa de erros.
- Extraia o campo `fact` e exiba em um card Bootstrap.
- Template em `flask_app/templates/catfact.html`.
- Em caso de erro de rede/JSON, mostre uma mensagem amigável na página.
- Inclua instruções de teste via navegador e curl.
- Atualize requirements.txt (requests) e forneça comando de instalação.
- Forneça uma mensagem de commit.
```

**Dificuldades a considerar:** timeouts; respostas malformadas; proxies/restrições de rede.

---

## 3) Página **`/hora`** com horário do computador do usuário (HTML5 + JS)
**Prompt funcional:**
```
Crie uma rota GET `/hora` que sirva uma página HTML5 mostrando o horário local do **navegador** (não do servidor).
- Use JavaScript (Date) para atualizar o relógio a cada 1 segundo.
- Ao passar o mouse sobre o horário, a cor muda (ex: de preto para vermelho) e volta ao sair do hover (CSS/JS).
- Coloque o template em `flask_app/templates/hora.html` e, se separar JS, use `flask_app/static/hora.js`.
- Forneça instruções de teste (abrir no navegador e verificar atualização/hover).
- Não introduza dependências Python novas.
- Mensagem de commit curta.
```

**Dificuldades a considerar:** garantir que a hora vem do client (JS); manter a página leve; sem libs externas desnecessárias.

---

## 4) Página **`/foto`** que ativa a câmera e tira foto (WebRTC)
**Prompt funcional:**
```
Implemente a rota GET `/foto` para servir uma página que:
- Usa `navigator.mediaDevices.getUserMedia({ video: true })` para ligar a câmera.
- Mostra o fluxo em um elemento <video>.
- Ao clicar no botão “Tirar Foto”, captura um frame para um <canvas> e exibe a imagem resultante abaixo.
- Ofereça um botão “Baixar foto” (download do canvas como PNG) sem enviar ao servidor.
- Arquivo do template: `flask_app/templates/foto.html`. Se separar JS, `flask_app/static/foto.js`.
- Documente que o acesso à câmera requer **contexto seguro** (HTTPS) ou `http://localhost` em navegadores modernos.
- Inclua instruções de teste e tratativa de permissão negada.
- Mensagem de commit curta.
```

**Dificuldades a considerar:** permissões de câmera e contexto seguro; UX se a permissão for negada; diferenças entre navegadores.

---

## 🔎 Prompts de **validação e verificação**
Use estes após cada implementação para garantir qualidade:

```
Revise o que você gerou e responda:
- Quais erros comuns podem ocorrer aqui? Mostre como tratá-los.
- Dê 3 formas de verificar que a funcionalidade está ok (curl, navegador, logs).
- Escreva testes manuais passo a passo para cada rota.
```
```
Gere uma coleção do Postman (JSON v2.1) com requisições GET para:
- http://localhost:5000/ (seu Flask raiz)
- http://localhost:5000/editorias
- http://localhost:5000/catfact
- http://localhost:5000/hora
- http://localhost:5000/foto
Inclua uma descrição curta em cada request.
```

---

## 🧹 Prompts de **refinamento**
```
Refatore o que você entregou para:
- Isolar configuração em um módulo settings/config se fizer sentido.
- Adicionar cabeçalhos de segurança básicos (X-Content-Type-Options, etc.) sem frameworks externos.
- Melhorar acessibilidade: contraste, labels e `aria-*` nos botões.
- Adicionar mini-guia de “Como rodar” e “Como verificar” no README do projeto.
```
```
Gere mensagens de commit semânticas (conventional commits) para cada mudança realizada.
```

---

## ✅ Resultado esperado
Com estes prompts, a IA deve retornar:
- Arquivos e **caminhos exatos** a criar/editar (templates, static, app.py).  
- **Código pronto** para uso, com explicações breves.  
- **Requirements** atualizados, comandos de instalação e execução.  
- **Passos de verificação** e (opcional) uma **coleção do Postman**.
