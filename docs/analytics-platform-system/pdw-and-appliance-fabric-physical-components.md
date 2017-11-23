---
title: "Malha de dispositivo e PDW componentes físicos (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7748d3da-0b7c-4ec6-9c22-4897758ba573
caps.latest.revision: "17"
ms.openlocfilehash: 93e4b1521b213c9d29f3cae9bcc900cad6c6a674
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="pdw-and-appliance-fabric-physical-components"></a>Componentes físicos de malha de dispositivo e PDW
Nomes e descrições para os componentes físicos de malha do PDW e dispositivo. A região PDW contém todos esses componentes.  
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagramas de componente  
Isso mostra os nomes dos componentes físicos e onde eles estão localizados no rack primeiro de um dispositivo do nó de computação de 6.  
  
![Nomes de componente de região PDW - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
O nome real para os componentes do PDW é o nome de região PDW, seguido por um traço, seguido pelo nome do componente. Por exemplo, se o nome da região PDW for PDW123, os nomes reais são **PDW123 CTL01**, **PDW123 CMP01**, etc.  
  
Da mesma forma, o nome real para componentes de malha do dispositivo é o domínio de aplicativo, seguido por um traço, seguido pelo nome do componente. Por exemplo, se o domínio de aplicativo é FSW123, a malha de dispositivo VMs são **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**, etc.  
  
Aqui está uma visão consolidada de uma região PDW com 6 nós de computação.  
  
![Nomes de componente do PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componentes do PDW  
As máquinas virtuais PDW fazem parte da região PDW.  
  
*PDW_region*-CTL01  
Uma máquina virtual que executa o nó de controle. Isso é executado em HST01 e pode fazer failover para HST02.  
  
> [!WARNING]  
> SQL Server PDW não oferece suporte à criação de um instantâneo da máquina virtual CTL01 usando o Gerenciador do Hyper-V. Instantâneos dependem do armazenamento local, o que causará erros se a máquina virtual tenta realizar failover para seu backup. Criando um instantâneo também pode causar problemas de confiabilidade com outra VM que o failover para o servidor passivo.  
  
*PDW_region*-CMP01 por meio de *PDW_Region*-CMP06  
Uma máquina virtual que executa o nó de computação. Neste diagrama de nó de computação 6, os hosts HSA01 HSA06 executados por meio de nó de computação VMs CMP01 por meio de CMP06 respectivamente.  
  
## <a name="fabric"></a>Componentes da malha de dispositivo  
Esses componentes são parte da malha de dispositivo.  
  
### <a name="virtual-machines"></a>Máquinas virtuais  
*appliance_domain*- WDS  
Este hosts de máquina virtual Windows implantação WDS (serviços), que usa o Analytics Platform System implantar sistemas operacionais Windows na rede do dispositivo. Ele também hospeda o serviço DHCP, que permite que os hosts de dispositivo ingressar na rede do dispositivo sem ter um endereço IP previamente configurado.  
  
O *appliance_domain*máquina de virtual - WDS é executado em HST01 e pode fazer failover para HST02. A máquina virtual WDS e a máquina virtual do VMM, implantar o Windows em hosts físicos durante a instalação do dispositivo. Durante o ciclo de vida do dispositivo, o WDS e o VMM executam operações como substituição de um host.  
  
*appliance_domain*- VMM  
O Virtual Machine Manager (VMM) é executado em uma máquina virtual e pode fazer failover para HST02. O VMM hospeda System Center para implantar o sistema operacional nos hosts físicos. O VMM também fornece o Windows Server Update Services (WSUS) para aplicar ou remover as atualizações do Windows em todos os hosts e máquinas virtuais.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Active Directory Domain Services, que contém o sistema de nome de domínio (DNS), é executado em uma máquina virtual em HST01 e HST02. Para alta disponibilidade do dispositivo de AD01 e AD02 são controladores de domínio replicados e eles não execute failover. Se um falhar, o outro já está disponível com os dados corretos.  
  
*appliance_domain*-ISCSI01  
Uma máquina virtual ISCSI é executado em cada um dos hosts com o armazenamento anexado (HSA01 HSA06). Essa VM não não failover.  
  
### <a name="hosts"></a>hosts  
*appliance_domain*-HST01 por meio de *appliance_domain*-HST06  
Os hosts para PDW controle nó e o dispositivo malha máquinas virtuais. HST03 é um host passivo opcional.  
  
*appliance_domain*-HSA01 por meio de *appliance_domain*-HSA08  
Os hosts com o armazenamento anexado (HSA). Cada HAS host executa uma VM do nó e em uma VM ISCSI.  
  
### <a name="cluster-for-pdw"></a>Cluster para PDW  
*appliance_domain*-WFOHST01  
O cluster PDW é denominado WFOHST01. Ele gerencia todos os hosts físicos e máquinas virtuais que pertencem ao PDW.  
  
### <a name="direct-attached-storage"></a>Armazenamento anexado direto  
*appliance_domain*-DAS01 por meio de *appliance_domain*-DAS03  
Este é o armazenamento com conexão direta que está conectado a nós de computação. HP tiver uma para todos os dois nós de computação. Dell e Quanta têm um para todos os três nós de computação.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configuração de dispositivo &#40; Analytics Platform System &#41;](appliance-configuration.md)  
[Tarefas de gerenciamento de dispositivo &#40; Analytics Platform System &#41;](appliance-management-tasks.md)  
  
