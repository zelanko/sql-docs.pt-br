---
title: Desinstalar hotfixes
description: Desinstale os hotfixes do Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399762"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar os hotfixes do Analytics Platform System 
As etapas a seguir descrevem como desinstalar um hotfix do sistema de plataforma de análise instalado anteriormente.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Pré-requisitos  
Para executar essas etapas, será necessário:  
  
-   Um logon do sistema de plataforma de análise com permissões para acessar o console de administração para monitorar o dispositivo.  
  
-   A conta de administrador de domínio para fazer logon no <em><appliance_domain nó></em> **-HST01** .  
  
-   O número do artigo da base de dados de conhecimento do hotfix a ser desinstalado.  
  
## <a name="to-uninstall-a-sql-server-pdw-hotfix"></a><a name="HowToUninstallPDW"></a>Para desinstalar um hotfix SQL Server PDW  
  
1.  Faça logon no nó <em><appliance_domain></em> **-HST01** como administrador de domínio de malha.  
  
2.  Use a opção Executar como administrador para abrir um prompt de comando.  
  
3.  Altere os diretórios `C:\PDWINST\Patches\<kbarticle>\media` para *<kbarticle>* onde é o número do artigo da base de dados de conhecimento do hotfix a ser desinstalado.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para remover o hotfix, execute o comando a seguir.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Baixar e aplicar as atualizações da Microsoft &#40;o sistema de plataforma de análise&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar o Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar hotfixes do sistema de plataforma de análise &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;o sistema de plataforma de análise&#41;](software-servicing.md)  
  
