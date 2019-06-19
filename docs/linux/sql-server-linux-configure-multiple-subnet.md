---
title: Configurar várias sub-redes grupos de disponibilidade AlwaysOn e instâncias de cluster de failover no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 4c8116462266386457270b16ebcdb684252f5dcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713260"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurar várias sub-redes grupos de disponibilidade AlwaysOn e instâncias de cluster de failover

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando uma instância de cluster sempre no grupo de disponibilidade (AG) ou do failover (FCI) abrange mais de um site, cada site geralmente tem seu próprio sistema de rede. Isso geralmente significa que cada site tem seu próprio endereçamento de IP. Por exemplo, endereços de sites do começam com 192.168.1. *x* e comece a endereços do Site B com 192.168.2. *x*, onde *x* é a parte do endereço IP que é exclusivo para o servidor. Sem algum tipo de roteamento em vigor na camada de rede, esses servidores não poderão se comunicar entre si. Há duas maneiras de lidar com esse cenário: configurar uma rede que conecta as duas sub-redes diferentes, conhecidas como uma VLAN, ou configurar o roteamento entre sub-redes.

## <a name="vlan-based-solution"></a>Solução baseada em VLAN
 
**Pré-requisito**: Para uma solução baseada em VLAN, cada servidor que participam de um grupo de disponibilidade ou FCI precisa de duas placas de rede (NICs) para disponibilidade adequada (uma porta dupla NIC seria um ponto único de falha em um servidor físico), para que ele pode ser atribuído a endereços IP em sua sub-rede nativo, bem como um na VLAN. Isso vai além de quaisquer outras necessidades de rede, como iSCSI, que também precisa de sua própria rede.

A criação de endereço IP para o grupo de disponibilidade ou FCI é feita na VLAN. No exemplo a seguir, a VLAN tem uma sub-rede de 192.168.3. *x*, portanto, o endereço IP criado para o grupo de disponibilidade ou FCI é 192.168.3.104. Nenhuma tarefa adicional precisará ser configurado, já que há um único endereço IP atribuído ao grupo de disponibilidade ou FCI.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configuração com o Pacemaker

No mundo do Windows, um Cluster de Failover do Windows Server (WSFC) nativamente dá suporte a várias sub-redes e lida com vários endereços IP por meio de uma dependência OR no endereço IP. No Linux, há nenhuma dependência OR, mas há uma forma de obter um várias sub-redes adequado nativamente com o Pacemaker, conforme mostrado a seguir. Você não pode fazer isso simplesmente usando a linha de comando normal do Pacemaker para modificar um recurso. Você precisará modificar as informações de cluster base (CIB). O CIB é um arquivo XML com a configuração do Pacemaker.

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

    Em que *filename* é o nome que você deseja chamar o CIB.

2.  Edite o arquivo que foi gerado. Procure o `<resources>` seção. Você verá os diversos recursos que foram criados para o grupo de disponibilidade ou FCI. Encontre o associado com o endereço IP. Adicionar um `<instance attributes>` seção com as informações para o segundo endereço IP, acima ou abaixo da existente, mas antes `<operations>`. Ele é semelhante à seguinte sintaxe:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    em que *NameForAttribute* é o nome exclusivo para este atributo *pontuação* é o número atribuído ao atributo, que deve ser maior do que a sub-rede primária, *RuleName*é o nome da regra, *ExpressionName* é o nome da expressão, *NodeNameInSubnet2* é o nome do nó em outra sub-rede, *NameForSecondIP* é o nome associado com o segundo endereço IP, *IPAddress* é o endereço IP para a segunda sub-rede, *NameForSecondIPNetmask* é o nome associado com a máscara de rede, e *Máscara de rede* é a máscara de rede para a segunda sub-rede.
    
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

3.  Importe o CIB modificado e reconfigurar o Pacemaker.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    em que *filename* é o nome do arquivo CIB com as informações de endereço IP modificados.

### <a name="check-and-verify-failover"></a>Verifique e verificar o failover

1.  Depois que o CIB é aplicada com êxito com a configuração atualizada, execute ping no nome DNS associado com o recurso de endereço IP no Pacemaker. Ele deve refletir o endereço IP associado à sub-rede que atualmente hospeda o grupo de disponibilidade ou FCI.
2.  Falha do grupo de disponibilidade ou FCI para a outra sub-rede.
3.  Depois que o grupo de disponibilidade ou FCI estiver totalmente online, execute ping no nome DNS associado ao endereço IP. Ele deve refletir o endereço IP na sub-rede do segundo.
4.  Se desejar, falhe o grupo de disponibilidade ou FCI para a sub-rede original.
