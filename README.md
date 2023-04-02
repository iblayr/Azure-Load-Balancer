# Azure Load Balancer
 
## Arquitetura



<p>Para criar o ambiente descrito, primeiro acessei o Portal do Azure e criei uma Virtual Network (VNET), com duas sub-redes (Subnets) dentro dela e um Grupo de Segurança de Rede (NSG) para controlar o acesso aos recursos. Em seguida, criei duas máquinas virtuais (VMs) usando a opção de Disponibilidade de Zona, para garantir alta disponibilidade e resiliência em caso de falhas.</p>

<p>Depois, criei um balanceador de carga (Load Balancer) e adicionei as duas VMs como Backend Pool, para distribuir o tráfego de rede entre elas. Também criei uma sonda de integridade (Health Probe) para monitorar a disponibilidade das VMs. Por fim, configurei um endereço IP público para o balanceador de carga, para que ele possa ser acessado a partir da Internet.</p>

<p>Para garantir que as VMs possam se comunicar com a Internet, criei um NAT de Origem (SNAT) para o Backend Pool. Isso permitirá que as VMs acessem a Internet sem ter que usar um endereço IP público dedicado para cada VM. No geral, esse ambiente oferece alta disponibilidade, escalabilidade e segurança para os aplicativos e serviços implantados no Azure.</p>


## Criar Virtual Network, Subnets e Network Security Group´




## Criar Virtual Machines utilizando Availability Zone




## Criar um Azure Load Balancer e adicionar as duas VMs como Backend Pool




## Criar SNAT para VMs do Backend Pool