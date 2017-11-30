---
title: "Propriedades do Servidor (página Geral) | Microsoft Docs"
ms.custom: 
ms.date: 06/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7ca680b434f4b483fb2f3cc3d99df5598a0766f1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="report-server-properties-general-page"></a>Propriedades do Servidor de Relatório (página Geral)
  Use essa página para exibir ou modificar o título usado no Gerenciador de Relatórios, habilitar ou desabilitar Meus Relatórios, selecionar uma definição de função para a segurança de Meus Relatórios e habilitar e desabilitar o controle de impressão do cliente.  
  
 **Para abrir esta página:**
 1) Iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) Conecte-se a uma instância do servidor de relatório.
 3) Clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**.  
  
 O modo de servidor determina quais propriedades de servidor você pode definir. Se você estiver gerenciando um servidor de relatório configurado para o modo integrado do SharePoint, você não poderá habilitar Meus Relatórios nem definir o título do portal da Web.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome que aparece na parte superior do portal da Web. Por padrão, esse valor é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. O nome que você especifica só aparece no Gerenciador de Relatórios.  
  
 **Versão**  
 Esta propriedade é somente leitura. Especifica a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que está sendo usada.  
  
 **Edição**  
 Esta propriedade é somente leitura. Especifica a instância do servidor de relatório atual. O Gerenciador de Relatório não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 **Modo de Autenticação**  
 Esta propriedade é somente leitura. Identifica os tipos de solicitações de autenticação aceitos pela instância do servidor de relatórios. Para alterar o modo de autenticação, você deve editar o arquivo **RSReportServer.config** . Para obter mais informações, consulte [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md).  
  
 **URL**  
 Esta propriedade é somente leitura. Especifica a URL para o serviço Web Servidor de Relatórios. Esse valor é especificado na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
 **Habilitar uma pasta Meus Relatórios para cada usuário**  
 Disponibilize **Meus Relatórios** aos usuários. Essa opção só está disponível para servidores de relatórios de modo nativo.  
  
 **Selecione a função a ser aplicada a cada pasta Meus Relatórios**  
 Especifique uma definição de função a ser usada na segurança de Meus Relatórios. A definição de função identifica o conjunto de tarefas que tem suporte em cada pasta Meus Relatórios.  

  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Habilitar e desabilitar Meus Relatórios](../../reporting-services/report-server/enable-and-disable-my-reports.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Proteger Meus Relatórios](../../reporting-services/security/secure-my-reports.md)  
  
  

