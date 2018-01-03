---
title: "Software de manutenção (Analytics Platform System)"
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
ms.assetid: cec4d924-c88f-470c-84bb-0af3e21aabf1
caps.latest.revision: "33"
ms.openlocfilehash: 8435291233a9486632f3d26ecae90c4bf1be8e21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="software-servicing"></a>Manutenção de software
Esta seção resume o software requisitos para dispositivos Analytics Platform System, incluindo os hotfixes do WSUS e Analytics Platform System de serviço.  
  
## <a name="Basics"></a>Noções básicas de manutenção de software  
**WSUS:** seu aparelho Analytics Platform System precisa ser configurado para receber atualizações do Windows Server Update Services (WSUS). Essas atualizações incluem alterações importantes para software de dispositivo. Depois de serem configurados, muitas atualizações instalarão automaticamente e não requerem gerenciamento manual. Normalmente, as atualizações do WSUS são configuradas durante o [configurar o Windows Server Update Services &#40; O WSUS &#41; &#40; Analytics Platform System &#41; ](configure-windows-server-update-services-wsus.md) etapa executada durante a instalação do novo dispositivo. Caso contrário, essa etapa de configuração pode ser executada posteriormente. Para obter informações sobre o WSUS, consulte o [site do WSUS guia](http://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Hotfixes:** Além disso, talvez seja necessário aplicar hotfixes Analytics Platform System. Um *hotfix* é uma atualização de software que é criada para um cliente específico resolver um problema com o software do sistema de plataforma de análise. Cada hotfix é um arquivo executável que instala a correção do problema específico do cliente. Cada hotfix também contém um acúmulo de todas as atualizações de software lançadas anteriormente para Windows, o SQL Server e o Analytics Platform System. Se você precisar instalar um hotfix, o suporte da Microsoft fornecerá o hotfix e as instruções.  
  
**Escopo de atualizações:** aplicar um hotfix ou service pack para o Analytics Platform System deve desligar o dispositivo inteiro. Ou seja, o PDW e HDInsight regiões serão afetados.  
  
**Adaptador de destino do SSIS e ferramentas de cliente:** ao aplicar um hotfix que inclui as alterações do MSI do SSIS destino adaptador ou MSI de ferramentas de cliente, em que os arquivos MSI serão atualizados o **C:\PDWINST\ClientTools** diretório no nó de controle. O hotfix não instala automaticamente os componentes dos arquivos MSI atualizados. Para atualizar esses componentes, o cliente deve desinstalar as versões antigas dos componentes e instalar novas versões dos arquivos MSI atualizados. Quando você desinstala um hotfix que inclui as alterações do MSI do SSIS destino adaptador ou MSI de ferramentas de cliente, os arquivos MSI para esses componentes será revertida para as versões anteriores. Para reverter esses componentes para uma versão anterior, o cliente deve desinstalar as versões existentes (mais recentes) dos componentes e reinstale as versões mais antigas dos arquivos MSI revertidos.  
  
## <a name="software-servicing-topics"></a>Tópicos de manutenção de software  
Os tópicos a seguir descrevem como gerenciar o serviço de software no dispositivo:  
  
-   [Baixe e aplique as atualizações da Microsoft &#40; Analytics Platform System &#41;](download-and-apply-microsoft-updates.md)  
  
-   [Desinstalar as atualizações da Microsoft &#40; Analytics Platform System &#41;](uninstall-microsoft-updates.md)  
  
-   [Aplicar Hotfixes do sistema de plataforma de análise &#40; Analytics Platform System &#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Desinstalar Hotfixes do sistema de plataforma de análise &#40; Analytics Platform System &#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
