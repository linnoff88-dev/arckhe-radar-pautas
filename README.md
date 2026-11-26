ï»¿# radar-pautas

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![radar-pautas ê¢â¬â as 6 pautas de IA do dia](guia/assets/banner.jpg)](https://inematds.github.io/radar-pautas/guia/)

**ê°Å¸â¡Â§ê°Å¸â¡Â· PortuguêÂªs êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

O radar-pautas êÂ© um script que lêÂª, de uma vez, cerca de 20 sites de notêÂ­cias de inteligêÂªncia artificial (blogs das empresas, imprensa, Hacker News, Reddit e os projetos que mais ganharam estrelas no GitHub na semana) e devolve as 6 pautas mais quentes das êÂºltimas 24 horas. Serve para quem produz conteêÂºdo e precisa decidir rêÂ¡pido o assunto do dia. Ele junta a mesma notêÂ­cia vinda de vêÂ¡rios sites, dêÂ¡ uma nota, confere se o link abre, avisa se vocêÂª jêÂ¡ fez algo parecido e, se pedir, sugere manchete, gancho e formato em portuguêÂªs. Precisa de Python 3; o GitHub CLI (`gh`) e o Claude Code sêÂ£o opcionais.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/radar-pautas/guia/**

## Usar

```bash
git clone https://github.com/inematds/radar-pautas ~/projetos/radar-pautas
cd ~/projetos/radar-pautas
python3 radar.py --dry          # olhar as 6 pautas sem gravar
python3 radar.py --angulos      # gravar + manchete/gancho/formato em PT (Claude Code)
```

Abra `~/projetos/output/radar-pautas/<data>/radar.html` no navegador.

| OpêÂ§êÂ£o | Faz |
|---|---|
| `--horas 48` | janela de tempo (padrêÂ£o 24) |
| `--n 8` | quantas pautas (padrêÂ£o 6) |
| `--angulos` | manchete, por que importa, gancho, formato e palavra, pelo `claude -p` (assinatura) |
| `--sem-github` | sem os repositêÂ³rios em alta |
| `--dry` | sêÂ³ imprime |

## O processo, do inêÂ­cio ao fim

ê°Å¸Â§Â  sessêÂ£o com o Nei êÂ· ê¢Å¡â¢ê¯Â¸Â script/timer êÂ· ê°Å¸Â¤â `claude -p` (assinatura)

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| 1 | Coleta | `radar.py` lêÂª os feeds de `fontes.json` em paralelo (e tenta de novo quando o site pede para esperar) + `gh search repos` | ê¢Å¡â¢ê¯Â¸Â |
| 2 | Junta e dêÂ¡ nota | mesma notêÂ­cia em vêÂ¡rios sites vira um assunto; nota por fontes, recêÂªncia, fonte oficial | ê¢Å¡â¢ê¯Â¸Â |
| 3 | Confere | abre o link de cada pauta (sêÂ³ entra com 200) e procura parecido no `PRODUCOES-VIDEO.md` | ê¢Å¡â¢ê¯Â¸Â |
| 4 | êângulo | `--angulos`: manchete PT, gancho, formato (r7ex/explicavideo/carrossel) e palavra | ê°Å¸Â¤â |
| 5 | Escolha | o Nei escolhe quais pautas viram vêÂ­deo ou carrossel | ê°Å¸Â§Â  |
| 6 | DiêÂ¡rio (opcional) | `systemd/radar-pautas.timer` êÂ s 07:30 ê¢â¬â **vem desligado**; ligar sêÂ³ com OK | ê¢Å¡â¢ê¯Â¸Â |

## Fontes

`fontes.json`: OpenAI, Google AI, Google DeepMind, Hugging Face, NVIDIA, Mistral, GitHub Blog, The Verge, TechCrunch, Ars Technica, Wired, The Decoder, MarkTechPost, MIT News, Simon Willison, Hacker News (150+ pontos), r/LocalLLaMA, Tecmundo, Canaltech e Olhar Digital (esses trêÂªs filtrados por palavras de IA). Testadas em 01/11/2026.

## Limites

- Feeds caem de vez em quando (um por rodada êÂ© normal); o resultado diz quais ficaram fora.
- O agrupamento êÂ© por palavras do têÂ­tulo: êÂ s vezes junta de menos (duas manchetes muito diferentes do mesmo fato).
- O êÂ¢ngulo vêÂª sêÂ³ têÂ­tulo e resumo: nêÂºmero e fato, sempre da fonte aberta.

LicenêÂ§a: MIT.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>