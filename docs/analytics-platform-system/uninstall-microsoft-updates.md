---
title: Desinstalar atualizações da Microsoft - Analytics Platform System | Microsoft Docs"
description: Desinstale as atualizações da Microsoft Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57d0eb3616cf3567f63d75029f79cea6709ed955
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Desinstalar as atualizações da Microsoft Analytics Platform System
Este artigo descreve como desinstalar uma atualização da Microsoft instalada anteriormente no dispositivo Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon Analytics Platform System com permissões para acessar o Console de administração para monitorar o dispositivo.  
  
-   Conhecimento da conta de administrador de domínio de malha para fazer logon na  *<Fabric Domain>*-HST01** nó.  
  
## <a name="HowToUninstallMSFT"></a>Para desinstalar as atualizações da Microsoft  
  
1.  Faça logon na  *<Fabric Domain>*-HST01** nó como o administrador de domínio de malha.  
  
2.  Para desinstalar todas as atualizações aprovadas para desinstalar o WSUS, abra uma janela de Prompt de comando e digite o seguinte comando. Substituir os itens de espaço reservado *< >* com as informações apropriadas.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte:
- [Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [Aplicar Hotfixes do sistema de plataforma de análise &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Desinstalar o Analytics Platform System Hotfixes &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
