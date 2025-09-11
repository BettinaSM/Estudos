## Validando se o usuário é local
grep -i *UserID* /etc/passwd;

## Expirando senha do usuário
sudo change -d 0 *UserID*;

## Mostrar ultima troca de senha e se esta exprada
sudo change -l *UserID*;

## Mostra status da conta
-> L ou LK = LOCK | P ou PS = Password Set

sudo passwd -S *UserID*;

## Validar tentativas invalidas
sudo pam_tally2 -u *UserID*;

sudo failog -u *UserID*;

sudo failock --user *UserID*;

# Valida tentativas invalidas e zera
sudo pam_tally2 -u *UserID* -r;

sudo failog -u *UserID* -r;

sudo failock --user *UserID* --reset;

## Desbloqueio de conta
sudo passwd -u *UserID*;

## Trocando senha
-> podemos fazer por comando e digitando a senha posteriormente:

sudo passwd *UserID*;

-> ou podemos fazer via hash:

sudo usermod -p '**senha_hash**' *UserID*;

## Cópia Hash
sudo grep usuario **/etc/shadow**;

-> ira aparecer algo como essa estrutura abaixo, o separador é o ":" que aparece apos o nome do usuario e antes da ultima data de troca da senha:

*UserID*:**senha_hash**:data_ultimo_troca:min:max:aviso:inativo:expira:reservado


## Criação de usuários
-> obs a home não necessariamente é home no ambiente, é possivel criar outros nomes/caminhos

sudo /user/sbin/useradd -c "gecos_da_sua_escolha" -d /home/*UserID* -s /bin/bash -p **hash** -g ***grupo*** -m *UserID*;

-> nesse caso usamos uma bash valida mas poderiamos colocar uma não valida para o usuario mesmo existindo não poder se conectar
      - /bin/bash = permite logar via ssh com senha ou chave RSA
      - /bin/nologin = não permite logar via ssh
      
-> a gecos é a informação imprtante para ficar salva no usuario, exemplo "usuario do time azul - resp bettina..."

-> setamos com uma senha via hash mas podemos não incluir, para isso seria necessaro remover da linha do comando -p **hash**

## Deleção de usuário
sudo userdel *UserID*;

## Validando se o user esta logado
who | grep *UserID*;

## Validando processos de usuario
ps -ef | grep -i *UserID*;

## User que senha não pode expirar ou trocar
-> comum em users de serviços

sudo passwd -x99999 -w7 -n7 *UserID*;

sudo change -M 99999 *UserID*;

sudo change -m 0 *UserID*;

## Validando grupo
groups *UserID*;

sudo grep -i  *UserID*; /etc/group

id *UserID*;

# Inclusão em Grupos
-> criando grupo

groupadd *nome_grupo*;

-> criando grupo com GID  fixo

groupadd -g **GID** *nome_grupo*;

->incluir usuario em grupo

sudo usermod -g *nome_grupo* **UserID**;

sudo gpasswd -a  **UserID** *nome_grupo*;

-> incluir grupos secundarios no usuario sem afetar demais

usermod -g *primary-group* -aG *second-group*,*other-group* **UserID**;

usermod -aG *second-group* **UserID**;

## Deletar grupo do /etc/group
delgroup *grupo*;

groupdel *grupo*;

## Privilegios no sudoers
-> validações de parametros no sudoers

sudo cat /etc/sudoers

sudo grep -i *palavra_chave* /etc/sudoers

-> edição, fazer backup antes de alterar

sudo visudo

-> backup e confirmação

cp -p /etc/sudoers /etc/sudoers.bkp

ls -l /etc/sudoers /etc/sudoers.bkp

## Chave RSA


## ACL Processos
# 1° Backup da ACL:
            find <diretorio> -type d -ls > path/diretorios
            find <diretorio> -type f -ls > path/arquivos

# 2 ° Verificar como esta a ACL
            getfacl

# 3° Realizar modificação na Acess Control List
            sudo find <diretorio> -xdev -type d -exec setfacl -m d:u:UserID:rwx,u:UserID:rwx {} \;
            sudo find <diretorio> -xdev -type f -exec setfacl -m u:UserID:rwx {} \;


-type d : diretório

-type f : file


d: : default - Somente em diretório

u : user

g : grupo

o : other

exemplo: <img width="474" height="245" alt="image" src="https://github.com/user-attachments/assets/753e18d0-036a-44f1-aed7-861eaab042c9" />


# Remove a ACL do path - Recursivo (b - remove / -R recusrsivo)
            setfacl -Rb /path/que/quer/remover/acl


# Restore de ACL
            setfacl --restore=/root/acl.backup

