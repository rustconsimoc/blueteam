# web/ — box **Web**

Captura de rede (`pcap.pcap`) de um segmento onde uma aplicação web foi comprometida.
A captura vai da fase de reconhecimento até a execução de comandos no servidor.

| Arquivo | Formato |
|---|---|
| `pcap.pcap` | libpcap, ~4,5 MB |

## Observações para a análise

- A captura contém **mais de uma sub-rede** e mais de um cliente conversando com o
  servidor. Nem todo tráfego presente faz parte do incidente: separe o que é atividade
  normal do que é atividade do atacante antes de tirar conclusões.
- Vale abrir tanto a visão de **conversas** (`Statistics → Conversations`) quanto o
  **Follow TCP Stream** dos fluxos relevantes.
- Requisições HTTP carregam parâmetros percent-encoded; decodifique-os antes de ler.

```bash
# panorama rápido
tshark -r pcap.pcap -q -z conv,ip
tshark -r pcap.pcap -Y 'http.request' -T fields -e ip.src -e http.request.full_uri
```
