---
title: Componentes físicos do dispositivo
description: Nomes e descrições para os componentes físicos do PDW e do Appliance Fabric.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400927"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>Componentes físicos do dispositivo – Analytics Platform System
Nomes e descrições para os componentes físicos do PDW e do Appliance Fabric. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagramas de componente  
Isso mostra os nomes dos componentes físicos e onde eles estão localizados no primeiro rack de um dispositivo de nó de 6 computadores.  
  
![PDW Region Component Names - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
O nome real para componentes do PDW é o nome da região do PDW, seguido por um traço, seguido pelo nome do componente. Por exemplo, se o nome da região do PDW for PDW123, os nomes reais serão **PDW123-CTL01**, **PDW123-CMP01**, etc.  
  
Da mesma forma, o nome real para componentes do Appliance Fabric é o domínio do dispositivo, seguido por um traço, seguido pelo nome do componente. Por exemplo, se o domínio do dispositivo for FSW123, as VMs do Appliance Fabric serão **FSW123-WDS**, **FSW123-AD01**, **FSW123-VMM**, etc.  
  
Aqui está uma exibição consolidada de uma região do PDW com 6 nós de computação.  
  
![Nomes dos componentes do PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componentes do PDW  
As máquinas virtuais do PDW fazem parte da região do PDW.  
  
*PDW_region*-CTL01  
Uma máquina virtual que executa o nó de controle. Isso é executado em HST01 e pode fazer failover para HST02.  
  
> [!WARNING]  
> SQL Server PDW não oferece suporte à criação de um instantâneo da máquina virtual CTL01 usando o Gerenciador do Hyper-V. Os instantâneos dependem do armazenamento local, o que causará erros se a máquina virtual tentar realizar o failover para o backup. A criação de um instantâneo também pode causar problemas de confiabilidade com as outras VMs que fazem failover para o servidor passivo.  
  
*PDW_region*-CMP01 por meio de *PDW_Region*-CMP06  
Uma máquina virtual que executa o nó de computação. Neste diagrama de seis nós de computação, os hosts HSA01 por meio do HSA06 executam VMs do nó de computação CMP01 por meio de CMP06, respectivamente.  
  
## <a name="fabric"></a>Componentes do Appliance Fabric  
Esses componentes fazem parte da malha do dispositivo.  
  
### <a name="virtual-machines"></a>Máquinas Virtuais  
*appliance_domain*-WDS  
Essa máquina virtual hospeda o WDS (serviços de implantação do Windows), que o sistema de plataforma de análise usa para implantar sistemas operacionais Windows na rede do dispositivo. Ele também hospeda o serviço DHCP, que permite que os hosts de dispositivo ingressem na rede do dispositivo sem ter um endereço IP pré-configurado.  
  
A máquina virtual *appliance_domain*-WDS é executada em HST01 e pode fazer failover para HST02. A máquina virtual do WDS e a máquina virtual do VMM, implantam o Windows nos hosts físicos durante a instalação do dispositivo. Durante o ciclo de vida do dispositivo, o WDS e o VMM executam operações como substituir um host.  
  
*appliance_domain*-VMM  
O Virtual Machine Manager (VMM) é executado em uma máquina virtual e pode fazer failover para HST02. O VMM hospeda o System Center para implantar o sistema operacional nos hosts físicos. O VMM também fornece Windows Server Update Services (WSUS) para aplicar ou remover atualizações do Windows em todos os hosts e máquinas virtuais.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Active Directory Domain Services, que contém o DNS (sistema de nomes de domínio), é executado em uma máquina virtual no HST01 e no HST02. Para alta disponibilidade do dispositivo, o AD01 e o AD02 são controladores de domínio replicados e não realizam failover. Se um falhar, o outro já estará disponível com os dados corretos.  
  
*appliance_domain*-ISCSI01  
Uma máquina virtual ISCSI é executada em cada um dos hosts com armazenamento anexado (HSA01-HSA06). Esta VM não faz failover.  
  
### <a name="hosts"></a>Hosts  
*appliance_domain*-HST01 por meio de *appliance_domain*-HST06  
Os hosts para as máquinas virtuais do nó de controle do PDW e da malha do dispositivo. HST03 é um host passivo opcional.  
  
*appliance_domain*-HSA01 por meio de *appliance_domain*-HSA08  
Os hosts com armazenamento anexado (HSA). Cada host tem uma VM de nó de computação e uma VM ISCSI.  
  
### <a name="cluster-for-pdw"></a>Cluster para PDW  
*appliance_domain*-WFOHST01  
O cluster PDW é chamado de WFOHST01. Ele gerencia todos os hosts físicos e máquinas virtuais que pertencem ao PDW.  
  
### <a name="direct-attached-storage"></a>Armazenamento anexado direto  
*appliance_domain*-DAS01 por meio de *appliance_domain*-DAS03  
Esse é o armazenamento de conexão direta que está conectado aos nós de computação. A HP tem um DAS para cada dois nós de computação. A Dell e a Quantity têm um DAS para cada três nós de computação.  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configuração do dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md)  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
