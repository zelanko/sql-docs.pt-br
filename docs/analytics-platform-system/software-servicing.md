---
title: Manutenção de software
description: Manutenção de software no sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400311"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Manutenção de software no Analytics Platform System
Esta seção resume os requisitos de manutenção de software para os dispositivos de análise da plataforma do Analytics, incluindo os hotfixes do WSUS e do sistema de plataforma de análise.  
  
## <a name="software-servicing-basics"></a><a name="Basics"></a>Noções básicas de manutenção de software  
**WSUS:** Seu dispositivo de sistema de plataforma de análise precisa ser configurado para receber atualizações do Windows Server Update Services (WSUS). Essas atualizações incluem alterações importantes no software do dispositivo. Depois de configuradas, muitas atualizações serão instaladas automaticamente e não exigirão gerenciamento prático. Normalmente, as atualizações do WSUS são configuradas durante a configuração [Windows Server Update Services &#40;WSUS&#41; &#40;o sistema de plataforma de análise&#41;](configure-windows-server-update-services-wsus.md) etapa executada durante a nova instalação do dispositivo. Caso contrário, essa etapa de configuração poderá ser executada mais tarde. Para obter informações sobre o WSUS, consulte o [Guia do site do WSUS](https://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Hotfixes:** Além disso, talvez seja necessário aplicar os hotfixes do Analytics Platform System. Um *hotfix* é uma atualização de software que é criada para um cliente específico para resolver um problema com o software de sistema de plataforma de análise. Cada hotfix é um arquivo executável que instala a correção para o problema específico do cliente. Cada hotfix também contém um acúmulo de todas as atualizações de software lançadas anteriormente para Windows, SQL Server e o sistema de plataforma de análise. Se você precisar instalar um hotfix, o suporte da Microsoft fornecerá o hotfix e as instruções.  
  
**Escopo das atualizações:** Aplicar um hotfix ou service pack ao sistema da plataforma de análise deve colocar todo o dispositivo offline.  
  
**Ferramentas de cliente e adaptador de destino SSIS:** Ao aplicar um hotfix que inclui alterações no MSI do adaptador de destino SSIS ou nas ferramentas de cliente, os arquivos MSI serão atualizados no diretório **C:\PDWINST\ClientTools** no nó de controle. O hotfix não instala automaticamente os componentes dos arquivos MSI atualizados. Para atualizar esses componentes, o cliente deve desinstalar as versões antigas dos componentes e instalar as novas versões dos arquivos MSI atualizados. Ao desinstalar um hotfix que inclui alterações no MSI do adaptador de destino SSIS ou nas ferramentas de cliente, os arquivos MSI para esses componentes serão revertidos para as versões anteriores. Para reverter esses componentes para uma versão anterior, o cliente deve desinstalar as versões existentes (mais recentes) dos componentes e reinstalar as versões mais antigas dos arquivos MSI revertidos.  
  
## <a name="software-servicing-topics"></a>Tópicos de manutenção de software  
Os tópicos a seguir descrevem como gerenciar a manutenção de software no dispositivo:  
  
-   [Baixar e aplicar as atualizações da Microsoft &#40;o sistema de plataforma de análise&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Desinstalar o Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [Aplicar hotfixes do sistema de plataforma de análise &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Desinstale os hotfixes do Analytics Platform System &#40;o Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
