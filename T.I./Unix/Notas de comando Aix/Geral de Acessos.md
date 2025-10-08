# Criação de user Local:
    sudo useradd -c "*Gecos_do usuario*" -d /home/usuario -s /usr/bin/ksh -g *grupo_user* -m **user_id**

# Alteração de senha:
    sudo passwd **user_id**

# Desbloqueio:
- Busca se existe tentativas de acesso sem sucesso

    lsuser -f UserID | grep unsuccessful_login_count ;

- Zera se existe tentativas de acesso sem sucesso
  
    sudo chsec -f /etc/security/lastlog -a "unsuccessful_login_count=0" -s UserID;
    sudo chsec -f /etc/security/lastlog -s UserID -a unsuccessful_login_count=0;

- Verifica se a conta está expirada

    sudo lsuser -f UserID |grep expires;

- Verificar se está lock

    sudo lsuser -f UserID |grep account_locked ;

# Reset de senha via SMIT:
smit user
<img width="590" height="273" alt="image" src="https://github.com/user-attachments/assets/a2a7b0f5-bf6b-424d-92ed-03dc18a84171" />

lock /unlock
<img width="850" height="175" alt="image" src="https://github.com/user-attachments/assets/9216051a-e233-47c9-bde9-72dbeb10f24d" />

coloca o user ali, dar enter
<img width="852" height="150" alt="image" src="https://github.com/user-attachments/assets/d4d525c5-e63a-4bbf-b7fe-acc9ebc47e91" />

Quanto tiver OK da um "ESC" e um "0" 

smit user
<img width="591" height="280" alt="image" src="https://github.com/user-attachments/assets/2e664f83-7aa8-429f-afbb-8ec3e77d5fd9" />

reset user`s failed
<img width="851" height="178" alt="image" src="https://github.com/user-attachments/assets/26301ad1-b2d3-4ac1-a008-953e53b12ccc" />

Coloca o nome do user
<img width="847" height="158" alt="image" src="https://github.com/user-attachments/assets/d14093c0-4792-4fa2-8880-bd564cff14e6" />

ESC 0 de novo. 

# Inclusão de grupo no usuario:
    useradd -G *grupo_user* **user_id**

nota: se ja tiver algum colocar junto do novo separados somente por virgulas ( ex: useradd -G *grupo1_user*,*grupo2_user* **user_id**)


# Forçando a criação de user LDAP em caso de erro de replicação do AD no AIX:

*Caso 1:  erro pela inexistencia de geração do usuario com defaul no arquivo necessario ou erro do parametro*

- Primeiro vamos ver as configurações bases do default:

    sudo lssec -f /etc/security/user -s default -a maxage -a SYSTEM

- Segundo vamos ver como esta para o usuario e se não esta bloqueado:

    lsuser -R LDAP ALL | grep -i **user_id**;

- Terceiro: vamos procurar ele no arquivo de permissionamento e se não aparecer vamos alterar manualmente os parametros para funcionamento:

    sudo vi /etc/security/user

colocar la dentro a informação abaixo

**user_id**:
        SYSTEM = "LDAP or files"
        maxage = 0


*Caso 2: o LDAP funcional mas não consegue nem criar a home e o user não consegue conectar*

- Executar os comandos Abaixo:

    chuser SYSTEM="LDAP or files" **user_id**
    mkdir -p /home/**user_id**
    chown -R **user_id**:*grupo_user* /home/**user_id**
    chmod -R 755 /home/**user_id**
    chsec -f /etc/security/lastlog -a unsccessful_login_count=0 -s **user_id**


# Corrigindo erro de acesso LDAP:

lsuser -R LDAP ALL | grep -i **user_id**;
lsuser -f **user_id** | grep unsuccessful_login_count ;
sudo chsec -f /etc/security/lastlog -a "unsuccessful_login_count=0" -s **user_id**;
sudo chsec -f /etc/security/lastlog -s **user_id** -a unsuccessfcul_login_count=0;
sudo lsuser -f **user_id** |grep expires;
sudo lsuser -f **user_id** |grep account_locked ;
sudo grep -i **user_id** /etc/security/user;
sudo lssec -f /etc/security/user -s default -a maxage -a SYSTEM
sudo lssec -f /etc/security/user -s default -a maxage -a SYSTEM
sudo chsec -f /etc/security/user -s default -a maxage=0 -a SYSTEM="LDAP or files"
sudo lssec -f /etc/security/user -s default -a maxage -a SYSTEM


