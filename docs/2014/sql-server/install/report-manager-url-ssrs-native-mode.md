---
title: URL do Gerenciador de relatórios (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f5e472f0cb8cb1a2fc8ed9d85b73622617a3a70a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63282045"
---
# <a name="report-manager-url-ssrs-native-mode"></a>URL do Gerenciador de Relatórios (modo nativo do SSRS)
  Use a página URL do Gerenciador de Relatórios para configurar ou modificar a URL usada para acessar o Gerenciador de Relatórios. Por padrão, a URL do Gerenciador de Relatórios herda o prefixo, o endereço IP e a porta da URL do serviço Web Servidor de Relatórios. Isso ocorre porque o Gerenciador de Relatórios fornece acesso front-end ao serviço Web que é executado no mesmo serviço do Servidor de Relatório. Se você estiver isolando os aplicativos de serviço e usando o Gerenciador de Relatórios para acessar um serviço Web Servidor de Relatórios em um computador diferente, deverá editar o arquivo RSReportServer.config para apontar o Gerenciador de Relatórios para uma instância diferente. Para obter mais informações sobre como configurar uma conexão do Gerenciador de relatórios para um servidor de relatório remoto, consulte [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Se estiver configurando o servidor de relatório para execução no modo integrado do SharePoint, não crie uma URL do Gerenciador de Relatórios. Não há suporte ao Gerenciador de Relatórios em um servidor de relatório que é executado no modo integrado do SharePoint. Se já existir uma URL para o Gerenciador de Relatórios, ela ficará indisponível depois que você configurar o servidor de relatório para execução no modo integrado do SharePoint.  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **URL do Gerenciador de Relatórios** no painel de navegação. Para obter mais informações sobre como iniciar o Configuration Manager, consulte [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!NOTE]  
>  Se o Gerenciador de Relatórios não estiver habilitado, você não poderá definir opções nessa página. Para obter mais informações sobre como habilitar o Gerenciador de relatórios, consulte [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Diretório virtual**  
 Especifica o nome do diretório virtual do Gerenciador de Relatórios. Você pode ter apenas um nome de diretório virtual para cada instância do Gerenciador de Relatórios no mesmo computador.  
  
 **URLs**  
 Exibe a URL definida para a instância atual do Gerenciador de Relatórios.  
  
 **Avançado**  
 Adicione mais uma URL à instância atual do Gerenciador de Relatórios.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [URLs em arquivos de configuração &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
