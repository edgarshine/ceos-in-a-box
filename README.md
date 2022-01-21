# ceos-in-a-box

PT-BR: Projeto pessoal para criar uma topologia de switching LS usando CEOS em um host CentOS  

Software base para o projeto

- Uma cópia de imagem Arista cEOS
- Vagrant
- Git
- instalação de ambiente virtualizado. O provider suporta VirtualBox e VMware Desktop/Fusion
  NOTA: Para VMware precisa instalar o plugin VMware para o Vagrant

## Instruções de instalação rápida

 1) clonar o projeto
 2) copiar uma imagem do cEOS dentro da pasta do projeto
 3) executar o comando "vagrant up"
 4) após instalação da VM ele pode ser acessado com o comando "vagrant ssh"
 5) acessando a VM, um ambiente de rede vitual pode ser criado usando a ferramenta Containerlab, que já é instalada na VM. Mais sobre o projeto ContainerLab: <https://containerlab.srlinux.dev/>
 6) criando um lab exemplo com 2 spines e 3 leafs: execute o comando "sudo containerlab deploy --topo ceos-small.yml"
 7) após a criação do ambiente, os switches podem ser acessados com o comando "sudo docker exec -ti \<nome do container\> login" , por exemplo "sudo docker exec -it clab-ceos-small-leaf1 login" , usuário padrão admin/admin
 8) os containers de host podem ser acessados com o comando "sudo docker exec -ti \<nome do host\> bash" , por exemplo "sudo docker exec -it clab-ceos-small-client1 bash"

## Operações específicas

- Para excluir o lab: "containerlab destroy --topo ceos-small.yml"
- Para suspender a VM: no prompt do laptop e na pasta do projeto "vagrant suspend" . Para reativar: "vagrant resume"

## Problemas operacionais e como sanar

### VMware

- Quando a VM é desativada manualmente, o plugin do Vagrant deixa de funcionar adequadamente. Reiniciar o plugin é uma forma de recuperar a operação da VM: <https://www.vagrantup.com/docs/providers/vmware/vagrant-vmware-utility>
