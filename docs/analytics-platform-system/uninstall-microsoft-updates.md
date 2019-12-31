---
title: Desinstalar atualizações da Microsoft
description: Desinstale as atualizações da Microsoft no sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399461"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Desinstalar as atualizações da Microsoft no Analytics Platform System
Este artigo descreve como desinstalar um Microsoft Update instalado anteriormente no dispositivo de sistema de plataforma de análise.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Pré-requisitos  
Para executar essas etapas, será necessário:  
  
-   Um logon do sistema de plataforma de análise com permissões para acessar o console de administração para monitorar o dispositivo.  
  
-   Conhecimento da conta do administrador de domínio da malha para fazer logon <em> <Fabric Domain> </em>no nó **-HST01** .  
  
## <a name="HowToUninstallMSFT"></a>Para desinstalar as atualizações da Microsoft  
  
1.  Faça logon no nó **-HST01** como administrador de domínio de malha. <em> <Fabric Domain> </em>  
  
2.  Para desinstalar todas as atualizações aprovadas para desinstalar o WSUS, abra uma janela de prompt de comando e insira o comando a seguir. Substitua os itens de espaço reservado *<  >* com as informações apropriadas.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte:
- [Baixar e aplicar as atualizações da Microsoft &#40;o sistema de plataforma de análise&#41;](download-and-apply-microsoft-updates.md) 
- [Aplicar hotfixes do sistema de plataforma de análise &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Desinstale os hotfixes do Analytics Platform System &#40;o Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Manutenção de software &#40;o sistema de plataforma de análise&#41;](software-servicing.md)  
  
