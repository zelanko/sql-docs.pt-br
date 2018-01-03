---
title: "Software antivírus (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60ab9a88-d339-4917-a38b-f9481aef38fd
caps.latest.revision: "29"
ms.openlocfilehash: 1733ec6be50d839284fa147eb1cf5c1660b77190
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="antivirus-software"></a>Software antivírus
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
  
***appliance_domain*-AD01** e  ***appliance_domain*-AD02**  
  
-   Sem restrições  
  
**VMs do nó de computação**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*- VMM**  
  
-   Sem restrições  
  
***appliance_domain*- WDS**  
  
-   Sem restrições  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Consulte Também  
[Tarefas de gerenciamento de dispositivo &#40; Analytics Platform System &#41;](appliance-management-tasks.md)  
  
