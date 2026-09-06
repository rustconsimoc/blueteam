# linux/ — box **Linux-Log**

Trecho de logs exportado de um servidor Ubuntu (`UBUNTU-WP47`) após um alerta do SOC.
Ambos os arquivos cobrem a **mesma janela** do dia 20/set, e o incidente atravessa os
dois: vale correlacionar.

| Arquivo | Origem | Formato |
|---|---|---|
| `auth.log` | `/var/log/auth.log` | syslog do `sshd` / `pam_unix` |
| `access.log` | `/var/log/apache2/access.log` | Apache *combined log format* |

## Observações para a análise

- Os carimbos de tempo do `access.log` já trazem o deslocamento de fuso (`-0300`).
  O `auth.log`, como todo syslog tradicional, **não registra fuso nem ano** — assuma
  o mesmo fuso do `access.log`.
- O `access.log` contém requisições de `::1` (loopback). São as
  `internal dummy connection` do próprio Apache, não fazem parte do tráfego externo.
- No `auth.log`, o `sshd` registra cada tentativa individualmente, e o `pam_unix`
  ainda emite uma linha de resumo por conexão ao encerrá-la. Contar as duas coisas
  como se fossem a mesma leva a números diferentes — decida qual evento você quer
  contar antes de rodar o `grep`.
