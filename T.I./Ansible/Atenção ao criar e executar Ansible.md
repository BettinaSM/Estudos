# Atenção necessaria antes de executar um Ansible

- verificar se é compativel com o os servidores que ira executar (nossos servidores no inventario.txt)
- sempre verificar se a sintax esta correta
  executar: ansible-playbook playbook.yml --syntax-check
- validar se o campo hosts do playbook esta com o mesmo parametro
- validar se as variaveis ou locais indicados estão no mesmo diretorio ou colocar o caminho absoluto



- outras possibilidades de validação de erros do playbook:
  Verificação de Sintaxe do Ansible Playbook

#### Modo de Verificação

O modo de verificação do Ansible permite que você execute um playbook sem fazer nenhuma alteração em seus sistemas. Isso é útil para testar e validar playbooks.

    ansible-playbook playbook.yml --check

No modo de verificação, o Ansible simulará a execução do playbook e reportará as alterações que ele teria feito.

#### Modo Diff

O modo Diff fornece comparações de antes e depois para tarefas que o suportam. Isso é útil para entender quais alterações serão feitas pelo playbook.

    ansible-playbook playbook.yml --check --diff

Combinar o modo de verificação com o modo de comparação fornece uma validação detalhada do seu manual, mostrando tanto as alterações que seriam feitas quanto as diferenças entre os estados atual e desejado.


** Considerações importantes

*Limitações do modo de verificação*: Alguns módulos podem não suportar totalmente o modo de verificação e podem não relatar possíveis alterações com precisão.

*Sensibilidade do modo de comparação*: O modo de comparação pode revelar informações confidenciais, portanto, use-o com cautela.

Usando essas opções, você pode validar completamente seus manuais do Ansible antes de aplicá-los aos seus sistemas, garantindo que estejam livres de erros e se comportem conforme o esperado.


  
