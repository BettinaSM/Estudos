### Chave RSA / Chave Trocada / Chave ssh / Relação de confiança
***Importante*** o tamanho da chave RSA em bits pode alterar dependendo do padrão de segurança, da versão do s.o., ou distro do linux

# Gerar chave ssh (RSA)

- Virar usuário "sudo su - [User ID que será gerado]"
  
      sudo su - UserID;
      cd ~ ; - ~ significa /home/conta/.ssh/
      pwd;
  
- Pegar chave gerada:
  
      cat /home/conta/.ssh/id_rsa.pub - Verifica se tem chave
      ssh-keygen -b 3072 -t rsa ; - Gera chave
      wc -l /home/conta/.ssh/id_rsa.pub; Verifica-se as linhas - Sempre tem que ter 1
  
- Pegar chave gerada: 

      cat /home/conta/.ssh/id_rsa.pub

- Verificar a permissão do arquivo, precisa ser 600
  
      /home/conta/.ssh/id_rsa.pub

# copiando / passando chave RSA
-modo simplificado: A chave RSA é enviada para o arquivo:  /home/conta/.ssh/authorized_keys

      ssh-copy-id -i ~/.ssh/id_rsa.pub login@servidor_destino

obs: é necessario que exista o arquivo destino no caminho absoluto

-caso não existir criar o arquivo authorized_keys , permissão 600 , se necessario criar o diretorio .ssh, permissão 700. 

** Podemos editar o arquivo  /home/conta/.ssh/authorized_keys e incluir a id_rsa.pub no servidor alvo para a troca de chave.**
