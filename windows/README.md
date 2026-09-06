# windows/ — box **Win**

Logs de evento exportados de um servidor Windows (`WIN10003`) após alertas do SOC
envolvendo endereços IP da internet.

| Arquivo | Canal | Eventos |
|---|---|---|
| `sec.evtx` | `Security` | autenticação (logon com e sem sucesso) |
| `sysmon.evtx` | `Microsoft-Windows-Sysmon/Operational` | conexões de rede (Event ID 3) |

## Observações para a análise

- **Fuso horário:** o EVTX grava `SystemTime` sempre em **UTC**. O Visualizador de
  Eventos do Windows converte para o fuso local da máquina que está abrindo o arquivo;
  ferramentas de linha de comando (`evtx_dump`, `python-evtx`) mostram o UTC cru.
  Fique atento a qual das duas você está lendo — a diferença é de horas.
- Os dois arquivos se complementam: o canal `Security` mostra o que aconteceu na
  autenticação, o Sysmon mostra quem estava conversando com a máquina e em quais portas.
- Nem todo IP que aparece é hostil, e nem todo evento de logon vem da rede.

```bash
# exemplo com python-evtx
pip install python-evtx
evtx_dump.py sec.evtx | less
```
