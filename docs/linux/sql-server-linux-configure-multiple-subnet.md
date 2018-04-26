---
title: Configurar várias sub-redes grupos de disponibilidade AlwaysOn e instâncias de cluster de failover no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 7d939a93e3a2ba9e2c2c59efa560d557842fde17
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurar várias sub-redes grupos de disponibilidade AlwaysOn e instâncias de cluster de failover

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando uma instância de cluster sempre na disponibilidade de grupo (AG) ou o failover (FCI) ocupar mais de um site, cada site geralmente tem seu próprio sistema de rede. Isso geralmente significa que cada site tem seu próprio endereçamento de IP. Por exemplo, endereços de sites do iniciam com 192.168.1. *x* e endereços do Site B começam com 192.168.2. *x*, onde *x* é a parte do endereço IP que é exclusivo para o servidor. Sem algum tipo de roteamento em vigor na camada de rede, esses servidores não poderão se comunicar entre si. Há duas maneiras para controlar este cenário: configurar uma rede que une duas sub-redes diferentes, conhecidas como uma VLAN, ou configurar o roteamento entre sub-redes.

## <a name="vlan-based-solution"></a>Solução baseada em VLAN
 
**Pré-requisito**: solução para uma VLAN, cada servidor participando de um grupo de disponibilidade ou FCI precisa de duas placas de rede (NICs) disponibilidade adequada (uma porta dupla NIC seria um ponto único de falha em um servidor físico), para que ele pode ser atribuído endereços IP sua sub-rede nativo como um na VLAN. Isso é além de quaisquer outras necessidades de rede, como iSCSI, que também precisa de sua própria rede.

A criação de endereço IP para o grupo de disponibilidade ou FCI é feita na VLAN. No exemplo a seguir, a VLAN tem uma sub-rede de 192.168.3. *x*, portanto, o endereço IP criado para o grupo de disponibilidade ou FCI é 192.168.3.104. Nenhuma tarefa adicional precisa ser configurado, pois há um único endereço IP atribuído ao grupo de disponibilidade ou FCI.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configuração com Pacemaker

No mundo do Windows, um Cluster de Failover do Windows Server (WSFC) nativamente dá suporte a várias sub-redes e lida com vários endereços IP por meio de uma dependência ou o endereço IP. No Linux, não há nenhuma dependência OR, mas há uma forma de obter um adequada várias sub-redes nativamente com Pacemaker, conforme mostrado a seguir. Você não pode fazer isso simplesmente usando a linha de comando Pacemaker normal para modificar um recurso. Você precisa modificar as informações de cluster base (CIB). O CIB é um arquivo XML com a configuração de Pacemaker.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Atualizar o CIB

1.  Exporte o CIB.

    **Red Hat Enterprise Linux (RHEL) e Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Onde *filename* é o nome que você deseja chamar o CIB.

2.  Edite o arquivo que foi gerado. Procure o `<resources>` seção. Você verá os vários recursos que foram criados para o grupo de disponibilidade ou FCI. Localize o item associado ao endereço IP. Adicionar um `<instance attributes>` seção com as informações para o segundo endereço IP acima ou abaixo da existente, mas antes `<operations>`. É semelhante à seguinte sintaxe:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    onde *NameForAttribute* é o nome exclusivo para esse atributo, *pontuação* é o número atribuído ao atributo, que deve ser maior que a sub-rede primária, *RuleName*é o nome da regra, *ExpressionName* é o nome da expressão, *NodeNameInSubnet2* é o nome do nó em outra sub-rede, *NameForSecondIP* é o nome associado com o segundo endereço IP, *IPAddress* é o endereço IP da sub-rede segundo, *NameForSecondIPNetmask* é o nome associado com a máscara de rede, e *Máscara de rede* é a máscara de rede para a sub-rede de segundo.
    
    O exemplo a seguir mostra um exemplo.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Importe o CIB modificado e reconfigurar Pacemaker.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    onde *filename* é o nome do arquivo CIB com as informações de endereço IP modificados.

### <a name="check-and-verify-failover"></a>Verifique e verificar o failover

1.  Depois que o CIB é aplicado com êxito com a configuração atualizada, execute ping o nome DNS associado ao recurso de endereço IP no Pacemaker. Ele deve refletir o endereço IP associado à sub-rede hospedando o grupo de disponibilidade ou FCI.
2.  Falha do grupo de disponibilidade ou FCI para a outra sub-rede.
3.  Depois que o grupo de disponibilidade ou FCI é totalmente online, execute ping o nome DNS associado ao endereço IP. Ele deve refletir o endereço IP na sub-rede segundo.
4.  Se desejar, fazer o grupo de disponibilidade ou FCI volta para a sub-rede original.
