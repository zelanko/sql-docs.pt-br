---
title: Software antivírus - Analytics Platform System | Microsoft Docs
description: Se seu data center requer o software antivírus, use estas diretrizes para instalar o software antivírus no sistema de plataforma de análise. É recomendável não instalar um software antivírus, a menos que seja um requisito sólido de seu data center.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5d9ff6848d2df43408613d41dc7a0e6f8c1b0b8c
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550037"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Software antivírus para Analytics Platform System
Se seu data center requer o software antivírus, use estas diretrizes para instalar o software antivírus no sistema de plataforma de análise. É recomendável não instalar um software antivírus, a menos que seja um requisito sólido de seu data center.  
  
> [!WARNING]  
> É altamente recomendável que você avalie individualmente o risco de segurança para cada computador em Analytics Platform System como um todo, e que você selecione as ferramentas apropriadas para o nível de risco de segurança de cada computador. Além disso, é recomendável que, antes de implementar qualquer projeto de proteção contra vírus, você testar a todo o sistema sob uma carga completa para avaliar as alterações no desempenho e estabilidade.  
>   
> Software de proteção contra vírus requer alguns recursos do sistema para executar. Você deve executar o teste antes e depois de instalar o software antivírus para determinar se há qualquer efeito no desempenho do sistema de plataforma de análise.  
  
Este tópico se baseia as orientações em [como escolher o software antivírus para execução em computadores que executam o SQL Server](http://support.microsoft.com/kb/309422) e [KB artigo 961804](http://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Lista de exclusões para Hosts físicos  
Para instalar o software antivírus em hosts físicos, exclua a seguinte lista de diretórios e processos. Eles não devem ser verificados pelo software antivírus.  
  
**Exclua esses diretórios:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V - diretório de configuração de máquina Virtual  
  
-   Discos rígidos C:\Users\Public\Documents\Hyper-V\Virtual - diretório da unidade de disco rígido virtual padrão  
  
-   C:\clusterStorage - diretórios de unidade de disco rígido Virtual  
  
**Exclua esses processos:**  
  
-   Gerenciamento de máquinas virtuais (Vmms.exe)  
  
-   Processos de trabalho de máquina virtual (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Lista de exclusões para máquinas virtuais (VMs)  
Para instalar o software antivírus nas máquinas virtuais, exclua a seguinte lista de diretórios e arquivos. Eles não devem ser verificados pelo software antivírus.  
  
***PDW_region*-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain *-AD01** e ***appliance_domain *-AD02**  
  
-   Sem restrições  
  
**VMs do nó de computação**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-VMM**  
  
-   Sem restrições  
  
***appliance_domain*-WDS**  
  
-   Sem restrições  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Consulte também  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
