# blueteam — evidências dos desafios (CTF SIMOC)

Repositório de **evidências** para as trilhas de Blue Team / análise forense do CTF SIMOC.
Cada pasta corresponde a uma box no RootTheBox. Aqui só há material bruto: nenhum
gabarito, nenhuma resposta.

## Estrutura

| Pasta | Box no CTF | Cenário |
|---|---|---|
| [`linux/`](linux/) | **Linux-Log** | Servidor Linux (Ubuntu) — logs de autenticação e de servidor web |
| [`web/`](web/) | **Web** | Captura de rede de um comprometimento de aplicação web |
| [`windows/`](windows/) | **Win** | Servidor Windows — logs de evento (EVTX) |

## Como baixar

Clonar o repositório inteiro:

```bash
git clone https://github.com/rustconsimoc/blueteam.git
```

Ou baixar apenas uma pasta pela interface do GitHub (botão **Code → Download ZIP**).

> **Atenção (Windows):** este repositório fixa `eol=lf` para os arquivos `.log` via
> `.gitattributes`. Se você extrair os logs por outro meio que não `git clone`,
> confira que as quebras de linha continuam sendo LF — alguns editores e o
> download em ZIP podem convertê-las e atrapalhar contagens automatizadas.

## Ferramentas sugeridas

- Logs texto: `grep`, `awk`, `sort`, `uniq`, `cut`
- Capturas de rede: [Wireshark / tshark](https://www.wireshark.org/)
- Logs de evento Windows: Visualizador de Eventos, [python-evtx](https://github.com/williballenthin/python-evtx), `evtx_dump`
- Consultas de atribuição: `whois`, RDAP, bases públicas de geolocalização de IP

## Integridade

Os hashes das evidências estão em [`CHECKSUMS.txt`](CHECKSUMS.txt). Confira antes de
começar a análise para garantir que os arquivos não foram alterados no transporte:

```bash
sha256sum -c CHECKSUMS.txt
```
