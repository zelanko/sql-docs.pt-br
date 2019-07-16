---
title: Componentes do dispositivo físicos – Analytics Platform System | Microsoft Docs
description: Nomes e descrições para os componentes físicos de malha do dispositivo e PDW.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fb7ad8715d3f7a885bc48f6bdcc7f1ec2842f269
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960422"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>Componentes do dispositivo físicos – Analytics Platform System
Nomes e descrições para os componentes físicos de malha do dispositivo e PDW. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagramas de componente  
Isso mostra os nomes dos componentes físicos e onde eles estão localizados no primeiro rack de um dispositivo de nó de computação de 6.  
  
![Nomes de componente de região PDW - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
O nome real para componentes do PDW é o nome de região PDW, seguido por um traço, seguido pelo nome do componente. Por exemplo, se o nome da região PDW for PDW123, os nomes reais são **PDW123 CTL01**, **PDW123 CMP01**, etc.  
  
Da mesma forma, o nome real para componentes de malha do dispositivo é o domínio de dispositivo, seguido por um traço, seguido pelo nome do componente. Por exemplo, se o domínio de dispositivo for FSW123, a malha appliance VMs estão **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**, etc.  
  
Aqui está uma exibição consolidada de uma região PDW com 6 nós de computação.  
  
![Nomes de componentes do PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componentes do PDW  
As máquinas virtuais PDW fazem parte da região PDW.  
  
*PDW_region*-CTL01  
Uma máquina virtual que executa o nó de controle. Isso é executado em HST01 e pode fazer failover para HST02.  
  
> [!WARNING]  
> SQL Server PDW não suporta a criação de um instantâneo da máquina virtual CTL01 usando o Gerenciador do Hyper-V. Instantâneos dependem de armazenamento local, o que causará erros se a máquina virtual tenta realizar failover para seu backup. Criando um instantâneo também pode causar problemas de confiabilidade com a outra VM que o failover para o servidor passivo.  
  
*PDW_region*-CMP01 por meio *PDW_Region*-CMP06  
Uma máquina virtual que executa o nó de computação. Neste diagrama de nó de computação 6, os hosts HSA01 HSA06 executados por meio do nó de computação VMs CMP01 por meio de CMP06, respectivamente.  
  
## <a name="fabric"></a>Componentes da malha de dispositivo  
Esses componentes são parte da malha do dispositivo.  
  
### <a name="virtual-machines"></a>Máquinas virtuais  
*appliance_domain*- WDS  
Este hosts de máquina virtual Windows Deployment Services (WDS), que usa o Analytics Platform System implantem os sistemas operacionais Windows na rede de dispositivo. Ele também hospeda o serviço DHCP, que permite que os hosts de dispositivo ingressar na rede do dispositivo sem a necessidade de um endereço IP configurado previamente.  
  
O *appliance_domain*máquina de virtual - WDS é executado em HST01 e pode fazer failover para HST02. A máquina de virtual do WDS e a máquina virtual do VMM, implante o Windows em hosts físicos durante a instalação do dispositivo. Durante o ciclo de vida do dispositivo, o WDS e o VMM executam operações como substituição de um host.  
  
*appliance_domain*-VMM  
O Virtual Machine Manager (VMM) é executado em uma máquina virtual e pode fazer failover para HST02. O VMM hospeda o System Center para implantar o sistema operacional nos hosts físicos. O VMM também fornece o Windows Server Update Services (WSUS) para aplicar ou remover as atualizações do Windows em todos os hosts e máquinas virtuais.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Serviços de domínio Active Directory, que contém o sistema de nome de domínio (DNS), é executado em uma máquina virtual em HST01 e HST02. Para alta disponibilidade do dispositivo, AD01 e AD02 são controladores de domínio replicado e eles não ocorrerá o failover. Se um falhar, outra já está disponível com os dados corretos.  
  
*appliance_domain*-ISCSI01  
Uma máquina virtual ISCSI é executado em cada um dos hosts com o armazenamento anexado (HSA01 HSA06). Essa VM não faz failover.  
  
### <a name="hosts"></a>Hosts  
*appliance_domain*-HST01 por meio *appliance_domain*-HST06  
Os hosts PDW controle nó e o dispositivo de malha das máquinas virtuais. HST03 é um host de passivo opcional.  
  
*appliance_domain*-HSA01 por meio *appliance_domain*-HSA08  
Os hosts com o armazenamento anexado (HSA). Cada HAS host executa uma VM do nó e em uma VM do ISCSI.  
  
### <a name="cluster-for-pdw"></a>Cluster para PDW  
*appliance_domain*-WFOHST01  
O cluster do PDW é denominado WFOHST01. Ele gerencia todos os hosts físicos e máquinas virtuais que pertencem ao PDW.  
  
### <a name="direct-attached-storage"></a>Armazenamento com conexão direta  
*appliance_domain*-DAS01 por meio *appliance_domain*-DAS03  
Isso é o armazenamento com conexão direta que está conectado a nós de computação. HP tiver uma para todos os dois nós de computação. A Dell e Quanta têm uma de todos os três nós de computação.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configuração de dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md)  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
