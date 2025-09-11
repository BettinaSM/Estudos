## interpretando as informações de diretorios e arquivos no linux
na imagem temos a interpretação das informações para diretorios e arquivos quanto a permissão, tipo, donos, nome data, tamanho
<img width="888" height="708" alt="image" src="https://github.com/user-attachments/assets/08c16964-4a2b-43ce-9248-0f34e1a0d748" />

## Alterando permissões
-> permissão de leitura, excrita e execução 
    - com numeros:
chmod 770 /caminho/completo;
. podemos setar permissionamentos com numeros conforme a tabela a seguir
<img width="456" height="499" alt="image" src="https://github.com/user-attachments/assets/3ca924ab-f355-416b-949a-649c983018ee" />

    - com  letras
    -> incluindo:
        chmod u+rwx /caminho/completo;

    -> removendo:
        chmod u-rwx /caminho/completo;

. o parametro u=usuario, g=grupo, o=outros
. podemos colocar outros parametros ou apenas alguns especifico; colocar vircula, sem espaço entre itens para mais de um, respeitando a ordem de privilegios

## Modificação de Owner e Group Owner: 
sudo chown userID:group /path/completo/

# Recursivo: #Recursividade (-R) - Irá realizar a ação tem todo os subdiretórios e arquivos
sudo chown -R userID:group /path/completo/

## Modificar somente group:
sudo chown :group /path/completo/

# Recursivo: #Recursividade (-R) - Irá realizar a ação tem todo os subdiretórios e arquivos
sudo chown -R :group /path/completo/

## Modificar somente owner:
sudo chown user: /path/completo/

# Recursivo: #Recursividade (-R) - Irá realizar a ação tem todo os subdiretórios e arquivos
sudo chown -R userID: /path/completo/


*links interessantes:*
https://medium.com/@chetxn/day-6-linux-file-permissions-and-access-control-lists-1b362b7a961
https://www.certificacaolinux.com.br/guia-completo-sobre-o-comando-chmod-no-linux-gerencie-permissoes-de-arquivos-e-diretorios/<img width="1152" height="82" alt="image" src="https://github.com/user-attachments/assets/ca52eabb-dfca-4ece-b16c-c7f4962d3c54" />
