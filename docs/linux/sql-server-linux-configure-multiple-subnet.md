---
title: Configurar o grupo de disponibilidade de várias sub-redes e a FCI (Linux)
description: Saiba como configurar grupos de disponibilidade Always On de várias sub-redes e FCIs (instâncias de cluster de failover) para o SQL Server em Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: f35f1916107e8ede0e7bf7cc3df483a0c33f3355
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558603"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurar instâncias de cluster de failover e grupos de disponibilidade Always On com várias sub-redes

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Quando um grupo de disponibilidade Always On ou FCI (instância de cluster de failover) abrange mais de um site, cada site geralmente tem sua própria rede. Isso geralmente significa que cada site tem seu próprio endereçamento IP. Por exemplo, os endereços do site A começam com 192.168.1.*x* e os endereços do site B começam com 192.168.2.*x*, em que *x* é a parte do endereço IP que é exclusiva para o servidor. Sem algum tipo de roteamento em vigor na camada de rede, esses servidores não poderão se comunicar entre si. Há duas maneiras de lidar com esse cenário: configurar uma rede que preencha as duas sub-redes diferentes, conhecidas como uma VLAN, ou configurar o roteamento entre as sub-redes.

## <a name="vlan-based-solution"></a>Solução baseada em VLAN
 
**Pré-requisito**: Para uma solução baseada em VLAN, cada servidor que participa de um grupo de disponibilidade ou FCI precisa de duas NICs (placas de rede) para disponibilidade adequada (uma NIC de porta dupla seria um ponto único de falha em um servidor físico), para que endereços IP possam ser atribuídos a esse servidor em sua sub-rede nativa, bem como um na VLAN. Isso se soma às outras necessidades de rede, assim como o iSCSI, que também precisa de sua própria rede.

A criação do endereço IP para o AG ou FCI é feita na VLAN. No exemplo a seguir, a VLAN tem uma sub-rede de 192.168.3.*x*, portanto, o endereço IP criado para o AG ou FCI é 192.168.3.104. Nenhuma configuração adicional é necessária, já que há um único endereço IP atribuído ao grupo de disponibilidade ou FCI.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configuração com o Pacemaker

No mundo do Windows, o WSFC (Cluster de Failover do Windows Server) dá suporte nativamente a várias sub-redes e manipula vários endereços IP por meio de uma dependência OR no endereço IP. No Linux, não há nenhuma dependência OR, mas há uma maneira de obter uma configuração com várias sub-redes adequada nativamente com o Pacemaker, conforme mostrado a seguir. Não é possível fazer isso simplesmente usando a linha de comando normal do Pacemaker para modificar um recurso. Você precisa modificar o CIB (base de informações do cluster). O CIB é um arquivo XML com a configuração do Pacemaker.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Atualize o CIB

1.  Exporte o CIB.

    **RHEL (Red Hat Enterprise Linux) e Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Em que *filename* é o nome pelo qual você deseja chamar o CIB.

2.  Edite o arquivo que foi gerado. Procure a seção `<resources>`. Você verá os vários recursos que foram criados para o AG ou o FCI. Localize aquele associado ao endereço IP. Adicione uma seção `<instance attributes>` com as informações para o segundo endereço IP acima ou abaixo do existente, mas antes de `<operations>`. Ela é semelhante à seguinte sintaxe:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    em que *NameForAttribute* é o nome exclusivo desse atributo, *Score* é o número atribuído ao atributo, que deve ser maior do que as sub-redes primárias, *RuleName* é o nome da regra, *ExpressionName* é o nome da expressão, *NodeNameInSubnet2* é o nome do nó na outra sub-rede, *NameForSecondIP* é o nome associado ao segundo endereço IP, *IPAddress* é o endereço IP para a segunda sub-rede, *NameForSecondIPNetmask* é o nome associado à máscara de rede e *Netmask* é a máscara de rede para a segunda sub-rede.
    
    Um exemplo é mostrado a seguir.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Importe o CIB modificado e reconfigure o Pacemaker.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    em que *filename* é o nome do arquivo do CIB com as informações de endereço IP modificadas.

### <a name="check-and-verify-failover"></a>Checar e verificar o failover

1.  Depois que o CIB for aplicado com êxito com a configuração atualizada, execute ping no nome DNS associado ao recurso de endereço IP no Pacemaker. Ele deve refletir o endereço IP associado à sub-rede que atualmente hospeda o grupo de disponibilidade ou o FCI.
2.  Faça failover do grupo de disponibilidade ou do FCI para a outra sub-rede.
3.  Depois que o grupo de disponibilidade ou o FCI estiver totalmente online, execute ping no nome DNS associado ao endereço IP. Ele deve refletir o endereço IP na segunda sub-rede.
4.  Se desejar, faça failback do grupo de disponibilidade ou FCI para a sub-rede original.
