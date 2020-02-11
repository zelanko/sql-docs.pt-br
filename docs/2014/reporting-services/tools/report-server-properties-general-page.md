---
title: Propriedades do Servidor (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93365925d412f672b9e8d3e5a9b5f67a850e508a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100010"
---
# <a name="server-properties-general-page"></a>Propriedades do Servidor (página Geral)
  Use essa página para exibir ou modificar o título usado no Gerenciador de Relatórios, habilitar ou desabilitar Meus Relatórios, selecionar uma definição de função para a segurança de Meus Relatórios e habilitar e desabilitar o controle de impressão do cliente.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do servidor de relatório, clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**.  
  
 O modo de servidor determina quais propriedades de servidor você pode definir. Se você estiver gerenciando um servidor de relatório configurado para modo integrado do SharePoint, não poderá habilitar Meus Relatórios nem definir o título do aplicativo para o Gerenciador de Relatórios.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite um nome de aplicativo exibido no Gerenciador de Relatórios. Por padrão, esse valor é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. O nome que você especifica só aparece no Gerenciador de Relatórios.  
  
 **Versão**  
 Essa propriedade é somente leitura. Especifica a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você está usando.  
  
 **Versão**  
 Essa propriedade é somente leitura. Especifica a instância do servidor de relatório atual. O Gerenciador de Relatório não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **Modo de autenticação**  
 Essa propriedade é somente leitura. Identifica os tipos de solicitações de autenticação aceitos pela instância do servidor de relatórios. Para alterar o modo de autenticação, você deve editar o arquivo RSReportServer.config. Para obter mais informações, consulte [Authentication with the Report Server](../security/authentication-with-the-report-server.md).  
  
 **URL**  
 Essa propriedade é somente leitura. Especifica a URL para o serviço Web Servidor de Relatórios. Esse valor é especificado na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
 **Habilitar uma pasta meus relatórios para cada usuário**  
 Disponibilize Meus Relatórios aos usuários. Essa opção só está disponível para servidores de relatórios de modo nativo.  
  
 **Selecione a função a ser aplicada a cada pasta meus relatórios**  
 Especifique uma definição de função a ser usada na segurança de Meus Relatórios. A definição de função identifica o conjunto de tarefas que tem suporte em cada pasta Meus Relatórios.  
  
 **Habilitar download para o controle de impressão do cliente ActiveX**  
 Define a propriedade do sistema  `EnableClientPrinting` de servidor de relatórios. Se você habilitar impressão de cliente, os usuários com permissões de administrador local têm a opção de baixar um controle ActiveX assinado para imprimir relatórios HTML. Para obter mais informações, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Habilitar e desabilitar meus relatórios](../report-server/enable-and-disable-my-reports.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Proteger Meus Relatórios](../security/secure-my-reports.md)  
  
  
