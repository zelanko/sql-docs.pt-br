---
title: Desinstalar o Analytics Platform System hotfixes no | Microsoft Docs
description: Desinstale o Analytics Platform System hotfixes.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 83e57a676ee0eff21eb3a736484d8e286cdeee01
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538776"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar o Analytics Platform System hotfixes 
As etapas a seguir descrevem como desinstalar um hotfix Analytics Platform System instalado anteriormente.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon Analytics Platform System com permissões para acessar o Console de administração para monitorar o dispositivo.  
  
-   A conta de administrador de domínio de logon para o *< appliance_domain > * * *-HST01** nó.  
  
-   O número de artigo de Base de dados de conhecimento do hotfix para desinstalar.  
  
## <a name="HowToUninstallPDW"></a>Para desinstalar um hotfix do SQL Server PDW  
  
1.  Faça logon na *< appliance_domain > * * *-HST01** nó como o administrador de domínio de malha.  
  
2.  Use a execução como a opção de administrador para abrir um Prompt de comando.  
  
3.  Altere os diretórios para `C:\PDWINST\Patches\<kbarticle>\media` onde *<kbarticle>* é o número do artigo da Base de conhecimento do hotfix para desinstalar.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para remover o hotfix, execute o comando a seguir.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Consulte também  
[Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar atualizações Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar Hotfixes do sistema de plataforma de análise &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
