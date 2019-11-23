---
title: URL de Report Manager (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dd4ff661a10eca71781aee9d1886e80936f6246d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952408"
---
# <a name="report-manager-url-ssrs-native-mode"></a>URL do Gerenciador de Relatórios (modo nativo do SSRS)
  Use a página URL do Gerenciador de Relatórios para configurar ou modificar a URL usada para acessar o Gerenciador de Relatórios. Por padrão, a URL do Gerenciador de Relatórios herda o prefixo, o endereço IP e a porta da URL do serviço Web Servidor de Relatórios. Isso ocorre porque o Gerenciador de Relatórios fornece acesso front-end ao serviço Web que é executado no mesmo serviço do Servidor de Relatório. Se você estiver isolando os aplicativos de serviço e usando o Gerenciador de Relatórios para acessar um serviço Web Servidor de Relatórios em um computador diferente, deverá editar o arquivo RSReportServer.config para apontar o Gerenciador de Relatórios para uma instância diferente. Para obter mais informações sobre como configurar uma conexão de Report Manager com um servidor de relatório remoto, consulte [ &#40;Gerenciador de configurações do Reporting Services modo&#41;nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Se estiver configurando o servidor de relatório para execução no modo integrado do SharePoint, não crie uma URL do Gerenciador de Relatórios. Não há suporte ao Gerenciador de Relatórios em um servidor de relatório que é executado no modo integrado do SharePoint. Se já existir uma URL para o Gerenciador de Relatórios, ela ficará indisponível depois que você configurar o servidor de relatório para execução no modo integrado do SharePoint.  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **URL do Gerenciador de Relatórios** no painel de navegação. Para obter mais informações sobre como iniciar o Configuration Manager, consulte [Gerenciador de configurações do Reporting Services &#40;modo&#41;nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!NOTE]  
>  Se o Gerenciador de Relatórios não estiver habilitado, você não poderá definir opções nessa página. Para obter mais informações sobre como habilitar Report Manager, consulte [ &#40;Gerenciador de configurações do Reporting Services&#41;modo nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Diretório virtual**  
 Especifica o nome do diretório virtual do Gerenciador de Relatórios. Você pode ter apenas um nome de diretório virtual para cada instância do Gerenciador de Relatórios no mesmo computador.  
  
 **URLs**  
 Exibe a URL definida para a instância atual do Gerenciador de Relatórios.  
  
 **Avançado**  
 Adicione mais uma URL à instância atual do Gerenciador de Relatórios.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [URLs em arquivos &#40;de configuração Configuration Manager&#41; SSRS](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
