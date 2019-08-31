---
title: Software antivírus-sistema de plataforma de análise (APS) | Microsoft Docs
description: Se seu data center exigir um software antivírus, use estas diretrizes para instalar o software antivírus no Analytics Platform System (APS). Recomendamos não instalar o software antivírus, a menos que seja um requisito de sua data center.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 92a34405e75c37cd0347b15aa445b98d84ebcc2a
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176058"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>Software antivírus para o Analytics Platform System (APS)
Se seu data center exigir software antivírus, use estas diretrizes para instalar o software antivírus no Analytics Platform System. Recomendamos não instalar o software antivírus, a menos que seja um requisito de sua data center.  
  
> [!WARNING]  
> É altamente recomendável que você avalie individualmente o risco de segurança para cada computador e para o sistema de plataforma de análise como um todo, e que você selecione as ferramentas apropriadas para o nível de risco de segurança de cada computador. Além disso, recomendamos que, antes de distribuir qualquer projeto de proteção contra vírus, você teste todo o sistema em uma carga completa para medir as alterações na estabilidade e no desempenho.  
>   
> O software de proteção contra vírus requer alguns recursos do sistema para serem executados. Você deve executar testes antes e depois de instalar o software antivírus para determinar se há algum efeito de desempenho no sistema da plataforma de análise.  
  
Este tópico se baseia na orientação de [como escolher o software antivírus para ser executado em computadores que executam o SQL Server e o](https://support.microsoft.com/kb/309422) [artigo 961804 do KB](https://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Lista de exclusões para hosts físicos  
Para instalar o software antivírus nos hosts físicos, exclua a lista de diretórios e processos a seguir. Eles não devem ser verificados pelo software antivírus.  
  
**Exclua estes diretórios:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-diretório de configuração da máquina virtual  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual discos rígidos – diretório de unidade de disco rígido virtual padrão  
  
-   C:\clusterStorage-diretórios de unidade de disco rígido virtual  
  
**Exclua estes processos:**  
  
-   Gerenciamento de máquinas virtuais (VMMS. exe)  
  
-   Processos de trabalho da máquina virtual (VMWP. exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Lista de exclusões para VMs (máquinas virtuais)  
Para instalar o software antivírus nas VMs, exclua a lista de diretórios e arquivos a seguir. Eles não devem ser verificados pelo software antivírus.  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01** e  **_appliance_domain_-AD02**  
  
-   Sem restrições  
  
**VMs do nó de computação**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   Sem restrições  
  
**_appliance_domain_-WDS**  
  
-   Sem restrições  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Consulte também  
[Sistema de plataforma &#40;de análise de tarefas de gerenciamento de dispositivo&#41;](appliance-management-tasks.md)  
  
