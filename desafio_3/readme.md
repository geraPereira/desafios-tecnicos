# Desafio 3 – Planejando um projeto de Media Player

A ideia é planejar o desenvolvimento de um media player capaz de:

- Reproduzir arquivos **MP4 (vídeo)** e **PNG (imagens)**.
- Exibir o conteúdo na **segunda tela do computador**.
- Permitir que o **usuário controle a duração e ordem** de exibição de cada item da playlist.

---


## 1. Entendimento do Projeto e Análise dos Requisitos

Primeiramente a ideia aqui é entender a proposta e elencar os requisitos funcionais e não funcionais do media player

Sendo os funcionais:

- Suporte a arquivos `.mp4` e `.png`.
- Reprodução em **modo tela cheia na segunda tela**.
- Interface para:
  - Modificar ordem da playlist (drag & drop ou botão ↑ ↓).
  - Definir duração de exibição de cada imagem (em segundos).
- Atualização da playlist **em tempo real** (sem reiniciar o app).
 
E os não funcionais:

- Rodar em qual sistema(s) operacional(is) 
- Operar x tempo sem travar (onde x é o número de horas ou minutos a ser definido e tempo a unidade de medida) 
- Baixa latência nas trocas 
- Logs de erro
- etc...

A partir dessa avaliação inicial podemos escolher a tecnoologia (linguagens e bibliotecas, além do banco de dados) e desenvolver a arquitetura a ser utilizada no projeto.

Assim dano início à POC ou ao MVP do projeto (a critério do gerente/tech lead).
---
