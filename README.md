# Voice Q&A Assistant (Whisper + Gemini + gTTS) — Google Colab

Projeto simples de perguntas e respostas por voz no Google Colab:
1) grava um áudio curto com uma pergunta,
2) transcreve com Whisper (rodando localmente),
3) gera resposta com a API do Gemini,
4) converte a resposta para áudio com gTTS.

## Demo (Notebook)
Abra e rode o notebook na pasta `notebooks/` (execute as células na ordem).
Dê permissão de microfone quando o navegador solicitar.

## Como funciona (pipeline)
- Gravação: usa JavaScript no Colab para capturar áudio do microfone e salvar `request_audio.wav`.
- ASR (Speech-to-Text): Whisper transcreve o áudio (ex.: modelo `small`).
- LLM: Gemini gera a resposta em texto a partir da transcrição.
- TTS: gTTS gera um arquivo `response_audio.mp3` com a resposta.

## Requisitos
### No Google Colab
- Você precisa instalar as dependências na primeira célula (pip + ffmpeg).
- O Whisper local requer o executável `ffmpeg` disponível no sistema (no Colab, normalmente basta instalar via `apt-get`). 

## Configurar a chave do Gemini (sem expor no código)
**Nunca** coloque sua API key direto no notebook para subir no GitHub.

Recomendado:
1. No Colab, abra o painel **Secrets** (ícone de chave).
2. Crie um secret chamado `GEMINI_API_KEY` com a sua chave.
3. No notebook, leia a variável/secret e inicialize o client.

Se você definir `GEMINI_API_KEY` (ou `GOOGLE_API_KEY`) como variável de ambiente, a chave pode ser detectada automaticamente pelas bibliotecas do Gemini; é recomendado definir apenas uma, e se ambas existirem, `GOOGLE_API_KEY` tem precedência.  
(Referência oficial: https://ai.google.dev/gemini-api/docs/api-key)

## Idiomas
- Whisper: use `language="pt"` (ou outro idioma) na transcrição para forçar o idioma do áudio.
- gTTS: use `lang="pt-br"` (ou outro código suportado) para a voz.

## Arquivos gerados
Durante a execução, o notebook gera arquivos de áudio (ex.: `.wav` e `.mp3`).
Eles não devem ser versionados no GitHub (veja `.gitignore`).
