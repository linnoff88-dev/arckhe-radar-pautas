# radar-pautas

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![radar-pautas â€” as 6 pautas de IA do dia](guia/assets/banner.jpg)](https://inematds.github.io/radar-pautas/guia/)

**ðŸ‡§ðŸ‡· PortuguÃªs Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O radar-pautas Ã© um script que lÃª, de uma vez, cerca de 20 sites de notÃ­cias de inteligÃªncia artificial (blogs das empresas, imprensa, Hacker News, Reddit e os projetos que mais ganharam estrelas no GitHub na semana) e devolve as 6 pautas mais quentes das Ãºltimas 24 horas. Serve para quem produz conteÃºdo e precisa decidir rÃ¡pido o assunto do dia. Ele junta a mesma notÃ­cia vinda de vÃ¡rios sites, dÃ¡ uma nota, confere se o link abre, avisa se vocÃª jÃ¡ fez algo parecido e, se pedir, sugere manchete, gancho e formato em portuguÃªs. Precisa de Python 3; o GitHub CLI (`gh`) e o Claude Code sÃ£o opcionais.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/radar-pautas/guia/**

## Usar

```bash
git clone https://github.com/inematds/radar-pautas ~/projetos/radar-pautas
cd ~/projetos/radar-pautas
python3 radar.py --dry          # olhar as 6 pautas sem gravar
python3 radar.py --angulos      # gravar + manchete/gancho/formato em PT (Claude Code)
```

Abra `~/projetos/output/radar-pautas/<data>/radar.html` no navegador.

| OpÃ§Ã£o | Faz |
|---|---|
| `--horas 48` | janela de tempo (padrÃ£o 24) |
| `--n 8` | quantas pautas (padrÃ£o 6) |
| `--angulos` | manchete, por que importa, gancho, formato e palavra, pelo `claude -p` (assinatura) |
| `--sem-github` | sem os repositÃ³rios em alta |
| `--dry` | sÃ³ imprime |

## O processo, do inÃ­cio ao fim

ðŸ§  sessÃ£o com o Nei Â· âš™ï¸ script/timer Â· ðŸ¤– `claude -p` (assinatura)

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| 1 | Coleta | `radar.py` lÃª os feeds de `fontes.json` em paralelo (e tenta de novo quando o site pede para esperar) + `gh search repos` | âš™ï¸ |
| 2 | Junta e dÃ¡ nota | mesma notÃ­cia em vÃ¡rios sites vira um assunto; nota por fontes, recÃªncia, fonte oficial | âš™ï¸ |
| 3 | Confere | abre o link de cada pauta (sÃ³ entra com 200) e procura parecido no `PRODUCOES-VIDEO.md` | âš™ï¸ |
| 4 | Ã‚ngulo | `--angulos`: manchete PT, gancho, formato (r7ex/explicavideo/carrossel) e palavra | ðŸ¤– |
| 5 | Escolha | o Nei escolhe quais pautas viram vÃ­deo ou carrossel | ðŸ§  |
| 6 | DiÃ¡rio (opcional) | `systemd/radar-pautas.timer` Ã s 07:30 â€” **vem desligado**; ligar sÃ³ com OK | âš™ï¸ |

## Fontes

`fontes.json`: OpenAI, Google AI, Google DeepMind, Hugging Face, NVIDIA, Mistral, GitHub Blog, The Verge, TechCrunch, Ars Technica, Wired, The Decoder, MarkTechPost, MIT News, Simon Willison, Hacker News (150+ pontos), r/LocalLLaMA, Tecmundo, Canaltech e Olhar Digital (esses trÃªs filtrados por palavras de IA). Testadas em 01/11/2026.

## Limites

- Feeds caem de vez em quando (um por rodada Ã© normal); o resultado diz quais ficaram fora.
- O agrupamento Ã© por palavras do tÃ­tulo: Ã s vezes junta de menos (duas manchetes muito diferentes do mesmo fato).
- O Ã¢ngulo vÃª sÃ³ tÃ­tulo e resumo: nÃºmero e fato, sempre da fonte aberta.

LicenÃ§a: MIT.

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>