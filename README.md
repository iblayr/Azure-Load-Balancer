# Azure Load Balancer
 
## Arquitetura

![Arquitetura](https://user-images.githubusercontent.com/25647623/229380898-8190967a-4c06-4510-ac6d-feaa6e2b9331.png)


<p>Para criar o ambiente descrito, primeiro acessei o Portal do Azure e criei uma Virtual Network (VNET), com duas sub-redes (Subnets) dentro dela e um Grupo de Segurança de Rede (NSG) para controlar o acesso aos recursos. Em seguida, criei duas máquinas virtuais (VMs) usando a opção de Disponibilidade de Zona, para garantir alta disponibilidade e resiliência em caso de falhas.</p>

<p>Depois, criei um balanceador de carga (Load Balancer) e adicionei as duas VMs como Backend Pool, para distribuir o tráfego de rede entre elas. Também criei uma Health Probe para monitorar a disponibilidade das VMs. Por fim, configurei um endereço IP público para o balanceador de carga, para que ele possa ser acessado a partir da Internet.</p>

<p>Para garantir que as VMs possam se comunicar com a Internet, criei um NAT de Origem (SNAT) para o Backend Pool. Isso permitirá que as VMs acessem a Internet sem ter que usar um endereço IP público dedicado para cada VM. No geral, esse ambiente oferece alta disponibilidade, escalabilidade e segurança para os aplicativos e serviços implantados no Azure.</p>


## Criar Virtual Network, Subnets e Network Security Group

* Criar VNET-WEB01

![001 - Criar VNET-WEB01](https://user-images.githubusercontent.com/25647623/229378236-0b79d2f5-a0bd-4696-84ad-1c6294f558db.png)

* Criar SUB-WEB01 e SUB-WEB02

![002 - Criar SUB-WEB01 e SUB-WEB02](https://user-images.githubusercontent.com/25647623/229378240-e5d5a35d-1f66-4521-b7f4-f44c8e408d64.png)

* Criar NSG-WEB01

![003 - Criar NSG-WEB01](https://user-images.githubusercontent.com/25647623/229378252-bed06625-20af-4aa3-ad67-c2cdd4fd21cc.png)

* Associar SUBNETs ao NSG

![004 - Associar subnets ao nsg](https://user-images.githubusercontent.com/25647623/229378270-5f20dd9f-949c-48ef-b9c7-7a2ba160fd19.png)

## Criar Virtual Machines utilizando Availability Zone

* Criar VM-WEB01

<img src="https://user-images.githubusercontent.com/25647623/229378430-aac1f2e7-5918-4e1d-9afe-13c00d73c9eb.png" width="500px"> <img src="https://user-images.githubusercontent.com/25647623/229378431-8b275adf-8cd3-45ef-9ef1-7caf40d272e8.png" width="500px">

* Criar VM-WEB02

<img src="https://user-images.githubusercontent.com/25647623/229378617-21dc05c1-5cb1-4037-a9f9-f26f9e34c9d8.png" width="500px"> <img src="https://user-images.githubusercontent.com/25647623/229378619-6015eaba-5d54-43cf-b011-97405afc8ea3.png" width="500px">


* Instalar o IIS nas VMs

<img src="https://user-images.githubusercontent.com/25647623/229378788-03de96b3-8d99-4f83-b4e5-13a283ffca76.png" width="500px"> <img src="https://user-images.githubusercontent.com/25647623/229378791-57279b7e-1569-472c-91b0-9b634deb5dfb.png" width="500px">

## Criar um Azure Load Balancer e adicionar as duas VMs como Backend Pool

* Criar Load Balancer LB-WEB01

![011 - Criar load balancer LB-WEB01](https://user-images.githubusercontent.com/25647623/229378987-c3be224d-1634-41a1-94bb-81952b563d46.png)

* Configurar Front-End IP para LB-WEB01

![012 - Configurar o frontend ip para o LB-WEB01](https://user-images.githubusercontent.com/25647623/229378995-e871ff99-b3c8-4b64-bd54-b2bbb5488173.png)

* Configurar Back-End Pool para LB-WEB01

![013 - Configurar Backend pool para LB-WEB01](https://user-images.githubusercontent.com/25647623/229379002-1cab2bd3-135d-4e41-bd7c-23b7617827a2.png)

* Criar Health Probe para LB-WEB01

![014 - Criar uma health probe para testar conexão http no LB-WEB01](https://user-images.githubusercontent.com/25647623/229379018-5f565ab6-8acf-42e5-87b4-8c80f80e3b5b.png)

* Criar regra de balanceamento

![015 - Criar regra de balanceamento no LB-WEB01](https://user-images.githubusercontent.com/25647623/229379044-7289b539-453e-4e63-8da8-22c309267a1c.png)

* Criar regra de entrada HTTP

![015 - Criar regra de entrada na porta 80 do nsg](https://user-images.githubusercontent.com/25647623/229379061-1a1ac9ba-359c-4475-9c6d-9c023b9651e4.png)

* Testar conexão (VM-WEB02)

![016 - Teste VM-WEB02](https://user-images.githubusercontent.com/25647623/229379085-8fc90e31-e626-4557-81e5-6f4397e95b5b.png)

* Parar IIS de uma das VMs (VM-WEB02) para testar Health Probe

![017 - Parando o IIS da VM-WEB02 para testar balanceamento](https://user-images.githubusercontent.com/25647623/229379147-7177417a-ec2c-4a0e-b02a-270b8adf8fba.png)

* Novo teste (VM-WEB01)

![018 - Teste VM-WEB01](https://user-images.githubusercontent.com/25647623/229379148-a30c9ad4-6ec6-4450-ab07-8c8274fb8628.png)

## Criar SNAT para VMs do Backend Pool

* Criar regra de saída SNAT no Load Balancer LB-WEB01

![021 - Criar regra de saída SNAT no load balancer LB-WEB01](https://user-images.githubusercontent.com/25647623/229379239-52bff061-1a9a-4220-ad47-9190571e7fcb.png)

* Configurar regra de saída SNAT para VMs no LB-WEB01

![022 - Configurar regra de saída SNAT para VMs no LB-WEB01](https://user-images.githubusercontent.com/25647623/229379266-3d24bfbc-ee16-449f-b2a1-ec94fbf4cedb.png)

* Testar ip saída VM-WEB01

![023 - Testar ip saída VM-WEB01](https://user-images.githubusercontent.com/25647623/229379286-cba14b96-2559-42dc-a235-5ebdeb1c32fa.png)

* Testar ip saída VM-WEB02

![024 - Testar ip saída VM-WEB02](https://user-images.githubusercontent.com/25647623/229379295-f6371c80-8a04-4669-b7d6-4493c39fff7f.png)
