---
title: Manutenção de software - Analytics Platform System | Microsoft Docs
description: Manutenção de software no Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 444d7f29e7f65da7e5d98dde310b2c1f8ad8dd4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678383"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Manutenção de software no Analytics Platform System
Esta seção resume o software de requisitos para dispositivos do Analytics Platform System, incluindo os hotfixes do WSUS e o Analytics Platform System de serviço.  
  
## <a name="Basics"></a>Noções básicas de manutenção de software  
**WSUS:** O dispositivo do Analytics Platform System precisa ser configurado para receber atualizações do Windows Server Update Services (WSUS). Essas atualizações incluem alterações importantes de software do dispositivo. Depois de serem configurados, muitas atualizações irá instalar automaticamente e não exigem gerenciamento prático. Normalmente, as atualizações do WSUS são configuradas durante o [configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41; ](configure-windows-server-update-services-wsus.md) etapa executada durante a instalação do novo dispositivo. Caso contrário, essa etapa de configuração pode ser executada mais tarde. Para obter informações sobre o WSUS, consulte o [site do WSUS guia](https://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Hotfixes:** Além disso, talvez você precise aplicar hotfixes do Analytics Platform System. Um *hotfix* é uma atualização de software que é criada para um cliente específico resolver um problema com o software do Analytics Platform System. Cada hotfix é um arquivo executável que instala a correção do problema específico do cliente. Cada hotfix também contém um acúmulo de todas as atualizações de software lançadas anteriormente para Windows, o SQL Server e o Analytics Platform System. Se você precisar instalar um hotfix, o suporte da Microsoft fornecerá o hotfix e instruções.  
  
**Escopo das atualizações:** Aplicar um hotfix ou service pack para o Analytics Platform System deve colocar o dispositivo inteiro offline.  
  
**Adaptador de destino do SSIS e ferramentas de cliente:** Ao aplicar um hotfix que inclui alterações para o SSIS destino adaptador MSI ou MSI do cliente de ferramentas, os arquivos MSI serão atualizados na **C:\PDWINST\ClientTools** diretório no nó de controle. O hotfix não instala automaticamente os componentes dos arquivos MSI atualizados. Para atualizar esses componentes, o cliente deve desinstalar as versões antigas dos componentes e instalar novas versões dos arquivos MSI atualizados. Quando você desinstala um hotfix que inclui alterações para o SSIS destino adaptador MSI ou MSI do cliente de ferramentas, os arquivos MSI desses componentes será revertido para as versões anteriores. Para reverter a esses componentes para uma versão anterior, o cliente deve desinstalar as versões existentes (mais recentes) dos componentes e reinstale as versões mais antigas dos arquivos MSI revertidos.  
  
## <a name="software-servicing-topics"></a>Tópicos de manutenção de software  
Os tópicos a seguir descrevem como gerenciar a manutenção de software no dispositivo:  
  
-   [Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Desinstalar atualizações da Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [Aplicar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Desinstalar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
