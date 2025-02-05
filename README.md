# DevOpsIAC
Projeto DevOps e Infraestrutura como Código (IaC)

## Descrição do Projeto
O objetivo deste projeto é desenvolver competências práticas em DevOps e Infraestrutura como Código (IaC) utilizando as ferramentas Vagrant e Ansible. Durante a execução do projeto, será provisionada uma infraestrutura virtual com configuração automatizada do sistema operacional e serviços essenciais.

## Integrantes
Camilly Pinto de Souza

## Disciplina

Administração de Sistemas e Abertos - **professor Pedro Batista de Carvalho Filho**


## Estrutura

### **1. Provisionamento da Infraestrutura com Vagrant**

*Características da VM:*

Provider: VirtualBox

Box: generic/debian12

Memória RAM: 1024 MB

Discos adicionais: 3 discos de 10 GB cada

Endereço IP: 192.168.57.10

Nome da VM: p01_Camilly_Nome02

*O arquivo Vagrantfile está devidamente configurado para atender a todas essas especificações.*

## 2. Configuração Automática com Ansible

*As seguintes tarefas foram automatizadas utilizando os playbooksansible criados:*
atualizarSO.yml   confLVM.yml  confSUDO.yml
BannerSSH.yml     confNFS.yml  criarUsers.yml
confHostname.yml  confSSH.yml  monitoraAcesso.yml
main_playbook.yml 

*2.1. Atualização do Sistema Operacional*

Realiza uma atualização completa de todos os pacotes do sistema. 

2.2. Configuração do Hostname

Altera o hostname da VM para p01-Camilly-Souza.

2.3. Criação de Usuários

Cria  usuários com logins correspondentes aos nomes dos integrantes do grupo.

2.4. Mensagem de Saudação

Configura uma mensagem exibida ao acessar o sistema via SSH:

> Acesso restrito apenas à pessoas com autorização expressa.
> Seu acesso está sendo monitorado!!!

*2.5. Configuração de SUDO*

Permite que os usuários do grupo ifpb tenham acesso de root utilizando o programa sudo.

*2.6. Configuração de SSH*

Permite apenas autenticação por chaves públicas.
Bloqueia o acesso ao root via SSH.
Restringe o acesso a usuários pertencentes ao grupo acesso_ssh.
Gera e configura chaves públicas para os usuários criados.

*2.7. Configuração de LVM*

Utiliza os 3 discos adicionais para criar um Volume Group (VG) chamado dados.

Cria um Logical Volume (LV) chamado sistema com tamanho de 15 GB.

Formata o LV sistema no formato ext4 e o monta automaticamente no diretório /dados utilizando o arquivo /etc/fstab.

*2.8. Configuração de NFS*

Configura o servidor NFS para compartilhar o diretório /dados/nfs com a rede 192.168.57.0/24.

Configurações adicionais:
Permitir escrita apenas para o usuário nfs-ifpb.
Mapear automaticamente qualquer usuário remoto para o usuário nfs-ifpb.
Forçar gravações imediatas no disco.
Remover o shell do usuário nfs-ifpb para aumentar a segurança.

*2.9. Monitoramento de Acesso*

Implementa um script (monitor_access.sh), localizado em [/usr/local/bin] que registra informações dos acessos no arquivo [/dados/nfs/acessos]:

Data e hora do acesso;
Nome de login do usuário;
Dispositivo TTY utilizado;
Endereço IP remoto.
Exemplo de entrada no arquivo:
2025-01-22 14:00; camilly; /dev/pts/0; 192.168.57.1

## Execução do Projeto

### Passos para Reproduzir:

Clone o repositório do projeto:

git clone https://github.com/camillysouza/projeto-devops.git
cd projeto-devops

Execute o provisionamento da VM com Vagrant:

vagrant up ou vagrant provision

Acesse a VM via SSH para verificar as configurações:

vagrant ssh

Certifique-se de que as tarefas automatizadas foram aplicadas com sucesso:

Verifique o hostname:

    hostname
    Teste as chaves SSH e a configuração de grupos.
    Valide o monitoramento de acessos e configuração de NFS.

## Estrutura do Repositório
*~/projeto:* diretório que engloba este projeto

    Vagrantfile: Arquivo para provisionamento da infraestrutura.

    playbooks/: Diretório contendo os playbooks e arquivos de configuração do Ansible.
            keys/: armazena as chaves publicas e privadas
    README.md: Documentação detalhada do projeto.

## Contato

Caso tenha dúvidas ou sugestões, entre em contato:

Email: camilly.p.souza@gmail.com

GitHub: github.com/camillysouza

Projeto desenvolvido como parte da disciplina de Administração de Sistemas Abertos no IFPB.
