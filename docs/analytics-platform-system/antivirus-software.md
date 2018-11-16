---
title: Software antivírus - Analytics Platform System | Microsoft Docs
description: Se seu data center exige um software antivírus, use estas diretrizes para instalar o software antivírus no Analytics Platform System. É recomendável não instalar o software antivírus, a menos que ele é um requisito sólido de seu data center.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2bf94fb04bd6f96de019c7e8543b8a626cebe439
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699106"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Software antivírus para o Analytics Platform System
Se seu data center exige um software antivírus, use estas diretrizes para instalar o software antivírus no Analytics Platform System. É recomendável não instalar o software antivírus, a menos que ele é um requisito sólido de seu data center.  
  
> [!WARNING]  
> É altamente recomendável que você avalie o risco de segurança para cada computador e para o Analytics Platform System, como um todo individualmente, e que você selecione as ferramentas que são apropriadas para o nível de risco de segurança de cada computador. Além disso, é recomendável que, antes de implementar qualquer projeto de proteção contra vírus, você teste todo o sistema sob uma carga completa para avaliar as alterações de estabilidade e desempenho.  
>   
> Proteção contra vírus requer alguns recursos do sistema para executar. Você deve executar testes antes e depois de instalar o software antivírus para determinar se há qualquer efeito de desempenho sobre o Analytics Platform System.  
  
Este tópico se baseia as diretrizes [como escolher o software antivírus seja executado em computadores que executam o SQL Server](https://support.microsoft.com/kb/309422) e [KB artigo 961804](https://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Lista de exclusões para Hosts físicos  
Para instalar o software antivírus em hosts físicos, exclua a seguinte lista de diretórios e os processos. Eles não devem ser verificados pelo software antivírus.  
  
**Exclua esses diretórios:**  
  
-   C:\programdata\microsoft\windows\hyper-v. - diretório de configuração de máquina Virtual  
  
-   Discos de rígidos C:\Users\Public\Documents\Hyper-V\Virtual - diretório padrão de unidade de disco rígido virtual  
  
-   C:\clusterStorage - diretórios de unidade de disco rígido Virtual  
  
**Exclua esses processos:**  
  
-   Gerenciamento de máquinas virtuais (Vmms.exe)  
  
-   Processos de trabalho de máquina virtual (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Lista de exclusões para máquinas virtuais (VMs)  
Para instalar o software antivírus em VMs, exclua a seguinte lista de diretórios e arquivos. Eles não devem ser verificados pelo software antivírus.  
  
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
  
