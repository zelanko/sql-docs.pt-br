---
title: O PowerPivot para SharePoint (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: c4c393d3-4856-47ac-ab5f-15da2f240d1d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1028dc0f73c6acb9832ce83bc5fad82e11322a13
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209853"
---
# <a name="powerpivot-for-sharepoint-ssas"></a>PowerPivot para SharePoint (SSAS)
  O PowerPivot para SharePoint é um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em execução no modo SharePoint. O PowerPivot para SharePoint fornece hospedagem de servidor de dados PowerPivot em um farm do SharePoint. Os dados PowerPivot são um modelo de dados analíticos que você cria usando um dos seguintes:  
  
-   O suplemento PowerPivot para Excel 2010  
  
-   Excel 2013  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 | [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010  
  
 O servidor que hospeda esses dados exige o SharePoint, os Serviços do Excel e uma instalação do PowerPivot para SharePoint. Os dados são carregados nas instâncias do PowerPivot para SharePoint, onde podem ser atualizados a intervalos agendados usando o recurso de atualização de dados PowerPivot que o servidor fornece para pastas de trabalho do Excel 2010 ou que os Serviços do Excel do SharePoint 2013 fornecem para as pastas de trabalho do Excel 2013.  
  
## <a name="powerpivot-for-sharepoint-2013"></a>PowerPivot para SharePoint 2013  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] oferece suporte ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] uso de Serviços do Excel do SharePoint 2013 de pastas de trabalho do Excel com modelos de dados e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatórios do Power View.  
  
 Os Serviços do Excel no SharePoint 2013 incluem a funcionalidade de modelo de dados para habilitar a interação com uma pasta de trabalho PowerPivot no navegador. Você não precisa implantar o suplemento PowerPivot para SharePoint 2013 no farm. Você só precisará instalar um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint e registrar o servidor nas configurações do **Modelo de Dados** dos Serviços do Excel.  
  
 A implantação do suplemento PowerPivot para SharePoint 2013 habilita a funcionalidade e os recursos adicionais no farm do SharePoint. Os recursos adicionais incluem Galeria PowerPivot, Atualização de Dados da Agenda e o Painel de Gerenciamento PowerPivot.  
  
 ![Implantação de servidor de modo 2 do PowerPivot do SSAS](../media/as-powerpivot-mode-2server-deployment.gif "implantação de servidor de modo 2 do PowerPivot do SSAS")  
  
## <a name="powerpivot-for-sharepoint-2010"></a>PowerPivot para SharePoint 2010  
 O PowerPivot para SharePoint 2010 fornece hospedagem de servidor de dados PowerPivot em um farm do SharePoint 2010. Os dados PowerPivot são um modelo de dados analíticos que você cria no Excel usando o suplemento PowerPivot para Excel. O servidor que hospeda esses dados exige o SharePoint 2010, os Serviços do Excel e uma instalação do PowerPivot para SharePoint. Os dados são carregados em instâncias do PowerPivot para SharePoint no farm, onde podem ser atualizadas em intervalos agendados usando o recurso de atualização de dados PowerPivot que o servidor fornece.  
  
### <a name="components-of-powerpivot-for-sharepoint-2010"></a>Componentes do PowerPivot para SharePoint 2010  
 O PowerPivot para SharePoint é implementado como um serviço compartilhado. Isso significa que os recursos internos e a infraestrutura podem ser usados para administrar, proteger e usar um aplicativo de serviço PowerPivot. A descoberta, o redirecionamento e o gerenciamento de conexão do servidor e do banco de dados são todos gerenciados no nível do farm. A Administração Central fornece a interface administrativa para os serviços usados para gerenciar a identidade de servidor, o estado de servidor e as propriedades de configuração.  
  
 Uma implantação completa do PowerPivot para SharePoint inclui componentes de cliente e servidor que se integram ao Excel e a Serviços do Excel em um farm do SharePoint. Os dados PowerPivot dentro de uma pasta de trabalho do Excel é um banco de dados do Analysis Services que exige um mecanismo analítico na memória xVelocity (VertiPaq) do Analysis Services para carregar e consultar os dados. Em uma estação de trabalho cliente, o mecanismo xVelocity é executado no processo dentro do Excel. Em um farm do SharePoint, o Analysis Services é executado em um servidor de aplicativos em que é emparelhado com serviços relacionados que manipulam solicitações para dados PowerPivot. O seguinte diagrama ilustra o cliente PowerPivot e os componentes de servidor:  
  
 ![GMNI_GeminiArch2](../media/gmni-geminiarch2.gif "GMNI_GeminiArch2")  
  
 O serviço Web PowerPivot é executado em um servidor de aplicativo Web. Ele redireciona solicitações do aplicativo Web para uma instância de Serviço de Sistema PowerPivot no farm.  
  
 O Serviço de Sistema PowerPivot emite solicitações de carregamento para o servidor do Analysis Services e gerencia conexões contínuas com dados que já estão carregados na memória, armazenando em cache ou descarregando os dados se eles não forem mais ser usados ou quando há contenção para recursos do sistema. Ele também acompanha a atividade do usuário. Os dados de integridade de servidor e outros dados de uso são coletados e apresentados em relatórios para indicar o funcionamento geral do sistema.  
  
 Uma instância de servidor do Analysis Services no modo Integrado do SharePoint conclui a implantação. Ele carrega, consulta e descarrega os dados. Ele também processará dados se a pasta de trabalho for configurada para atualização de dados PowerPivot.  Cada instância está acoplado ao Serviço de Sistema PowerPivot local que faz parte da mesma instalação.  
  
##  <a name="bkmk_RelatedContent"></a> Nesta seção  
 [Administração e configuração de servidor do PowerPivot na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Configuração do PowerPivot usando o Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [Ferramentas de Configuração do PowerPivot](power-pivot-configuration-tools.md)  
  
 [Autenticação e autorização PowerPivot](power-pivot-authentication-and-authorization.md)  
  
 [Regras de integridade do PowerPivot - configurar](configure-power-pivot-health-rules.md)  
  
 [Painel de Gerenciamento PowerPivot e dados de uso](power-pivot-management-dashboard-and-usage-data.md)  
  
 [A Galeria PowerPivot](../../2014-toc/books-online-for-sql-server-2014.md)  
  
 [Acesso a dados PowerPivot](power-pivot-data-access.md)  
  
 [Atualização de dados PowerPivot](power-pivot-data-refresh.md)  
  
 [Feeds de dados PowerPivot](power-pivot-data-feeds.md)  
  
 [Conexão de modelo semântico de BI do PowerPivot &#40;. bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)  
  
 **Nas outras seções**  
  
## <a name="additional-topics"></a>Tópicos adicionais  
 [Atualizar o PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)  
  
 [Instalação do PowerPivot para SharePoint 2013](../instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [Referência do PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
 [Topologias de licença de exemplo e custos para autoatendimento de Business Intelligence do SQL Server 2014](../../sql-server/install/example-license-topologies-costs-self-service-business-intelligence.md)  
  
## <a name="see-also"></a>Consulte também  
 [Implantação e planejamento do PowerPivot](http://go.microsoft.com/fwlink/?linkID=220972)   
 [Recuperação de desastres para PowerPivot para SharePoint](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
