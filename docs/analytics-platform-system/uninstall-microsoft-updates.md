---
title: Desinstalar atualizações da Microsoft - Analytics Platform System | Microsoft Docs"
description: Desinstale atualizações da Microsoft Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4739d05b1878c8b7fc9f66f2e0b8145ff1044e54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243831"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Desinstalar atualizações da Microsoft no Analytics Platform System
Este artigo descreve como desinstalar uma atualização instalada anteriormente no dispositivo do Analytics Platform System da Microsoft.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon do Analytics Platform System com permissões para acessar o Console de administração para monitorar o dispositivo.  
  
-   Dados de Conhecimento da conta de administrador de domínio de malha para fazer logon na <em> <Fabric Domain> </em> **-HST01** nó.  
  
## <a name="HowToUninstallMSFT"></a>Para desinstalar as atualizações da Microsoft  
  
1.  Faça logon na <em> <Fabric Domain> </em> **-HST01** nó como o administrador de domínio do Fabric.  
  
2.  Para desinstalar todas as atualizações são aprovadas para o WSUS desinstalar, abra uma janela de Prompt de comando e digite o seguinte comando. Substitua os itens de espaço reservado *< >* com as informações apropriadas.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte:
- [Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [Aplicar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Desinstalar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
