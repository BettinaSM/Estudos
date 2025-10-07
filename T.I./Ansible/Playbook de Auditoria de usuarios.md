## Playbook de auditoria de usuarios:

O playbook trata-se de uma validação nos ambientes linux e aix, que possuem acessos locais e ldap para questões de auditoria e validação dos usuarios e privilegios no ambiente.
Nele vamos validar se o user ldap esta ativo ou se o usuario é local, grupos e privilegios no sudoers.

- estrutura:

inventario_hosts.txt     # lista de hosts (inventário ansible - ja existe mas talvez falte servidor)

user.txt                 # contém a variável user (nome do usuário a ser auditado)

playbook.yml             # playbook principal

resultados            # diretorio onde as wo seram registradas (sera pedido) e cada 1 tera 5 arquivos


- Ao executar teremos a seguinte organixação para cada incidente setado:

resultados/

  INCxxxxx/
  
    usuario_ldap
    
    usuario_local
    
    presente_group
    
    privilegio_sudoers
    
    remocao_ok
    

Obs uma melhoria seria deixar separado para cada usuario em especifico mas assim ele ja separa o todo indicando o usuario no arquivo criado do que ainda é necessario remover
