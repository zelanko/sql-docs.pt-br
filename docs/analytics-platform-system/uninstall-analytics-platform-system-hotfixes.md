---
title: Desinstalar o Analytics Platform System Hotfixes (Analytics Platform System)
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
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: "21"
ms.openlocfilehash: 32d733f2e05855eb361095d23d6c34acefd343dc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar Hotfixes do sistema de plataforma de análise
As etapas a seguir descrevem como desinstalar um hotfix Analytics Platform System instalado anteriormente.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon Analytics Platform System com permissões para acessar o Console de administração para monitorar o dispositivo.  
  
-   A conta de administrador de domínio de logon para o *< appliance_domain >***-HST01** nó.  
  
-   O número de artigo de Base de dados de conhecimento do hotfix para desinstalar.  
  
## <a name="HowToUninstallPDW"></a>Para desinstalar um hotfix do SQL Server PDW  
  
1.  Faça logon na *< appliance_domain >***-HST01** nó como o administrador de domínio de malha.  
  
2.  Use a execução como a opção de administrador para abrir um Prompt de comando.  
  
3.  Altere os diretórios para `C:\PDWINST\Patches\<kbarticle>\media` onde  *<kbarticle>*  é o número do artigo da Base de conhecimento do hotfix para desinstalar.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para remover o hotfix, execute o comando a seguir.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Baixe e aplique as atualizações da Microsoft &#40; Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar as atualizações da Microsoft &#40; Analytics Platform System &#41;](uninstall-microsoft-updates.md)  
[Aplicar Hotfixes do sistema de plataforma de análise &#40; Analytics Platform System &#41;](apply-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40; Analytics Platform System &#41;](software-servicing.md)  
  
