## Contrab
  -> executar comandos como root ou com usuario em especifico que tem acesso a crontab e com o agendamento desejado para alteração

# Listar agendamentos do usuário atual
crontab -l;

# Filtrar no list do contrab
crontab -l | grep '**palavra_chave**';

# Editar agendamentos do usuário atual
crontab -e;

# Remover todos os agendamentos do usuário atual
  -> cuidado apaga tudo sem perguntar:
contrab -r;
  -> pergunta antes de apagar:
crontab -i -r;

# Instalar um arquivo como crontab do usuário
  -> Substitui a crontab atual pelo conteúdo do arquivo
crontab nome_arquivo;

# Editar/Listar a crontab de outro usuário (como root)
crontab -u usuario -e;   # editar
crontab -u usuario -l;   # listar


# Acesso crontab 
  -> Colocar o nome do usuario no documento na linha debaixo (usar vi):
/etc/cron.allow

(link de apoio: https://www.thegeekdiary.com/how-to-allow-only-specific-non-root-users-to-use-crontab/)

====

🔹 **Estrutura da linha do crontab**
  -> Cada linha segue o formato: MIN HORA DIA_MÊS MÊS DIA_SEMANA comando

MIN -> munutos (0-59)
HORA -> horas (0-23)
DIA_MÊS -> dia do mês (1-31)
MÊS -> mês (1-12)
DIA_SEMANA -> dia da semana (0-6, onde 0=domingo)
comando -> oque será executado

===

🔹 **Diretórios especiais do cron**

Além do crontab, alguns diretórios permitem agendamento automático:

/etc/cron.hourly/ → scripts executados 1x por hora
/etc/cron.daily/ → scripts executados 1x por dia
/etc/cron.weekly/ → scripts executados 1x por semana
/etc/cron.monthly/ → scripts executados 1x por mês

===

🔹**Arquivos globais do cron**

/etc/crontab → crontab do sistema (permite definir usuário para rodar o comando).
/etc/cron.d/ → arquivos adicionais de agendamento.
/etc/cron.allow e /etc/cron.deny → controlam quem pode usar crontab.

===
🔹 **Verificando execução dos jobs**
  ->Logs de execução:
grep CRON /var/log/cron;

ou em sistemas com systemd:
journalctl -u cron;
journalctl -u crond;
