---
title: Desinstalar hotfixes do Analytics Platform System no | Microsoft Docs
description: Desinstale hotfixes do Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5507eae7bb2f8a5ce138223a031ac4946d9f0030
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62675672"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar hotfixes do Analytics Platform System 
As etapas a seguir descrevem como desinstalar um hotfix para o Analytics Platform System instalada anteriormente.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
Para executar essas etapas, você precisará de:  
  
-   Um logon do Analytics Platform System com permissões para acessar o Console de administração para monitorar o dispositivo.  
  
-   A conta de administrador de domínio para fazer logon para o <em>< appliance_domain ></em>**-HST01** nó.  
  
-   O número de artigo de conhecimento do hotfix para desinstalar.  
  
## <a name="HowToUninstallPDW"></a>Para desinstalar um hotfix do SQL Server PDW  
  
1.  Faça logon na <em>< appliance_domain ></em>**-HST01** nó como o administrador de domínio do Fabric.  
  
2.  Use a execução como opção de administrador para abrir um Prompt de comando.  
  
3.  Altere os diretórios para `C:\PDWINST\Patches\<kbarticle>\media` onde *<kbarticle>* é o número de artigo da Base de conhecimento do hotfix para desinstalar.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para remover o hotfix, execute o comando a seguir.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Consulte também  
[Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar atualizações da Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
