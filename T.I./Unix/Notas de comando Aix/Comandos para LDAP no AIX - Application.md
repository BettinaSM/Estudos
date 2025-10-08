# Parar | Stop
    /usr/sbin/stop-secldapclntd

# Iniciar | Start
    /usr/sbin/start-secldapclntd

# Restart 1
    /usr/sbin/stop-secldapclntd ; /usr/sbin/start-secldapclntd

# Para validar se está rodando | validate if it's running:
    lssrc -a | grep ldap

# RESTART 2
    /usr/sbin/restart-secldapclntd

*fonte:* https://www.ibm.com/docs/en/aix/7.2?topic=r-restart-secldapclntd-command<img width="799" height="431" alt="image" src="https://github.com/user-attachments/assets/ec097bc2-0ac2-4e90-919a-cbf583b050c0" />
