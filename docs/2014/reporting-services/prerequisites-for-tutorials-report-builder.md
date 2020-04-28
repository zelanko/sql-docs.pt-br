---
title: Pré-requisitos para tutoriais (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 17c8b67d29cb82956a37bc3f83867161486a4f9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73637863"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>Pré-requisitos para tutoriais (Construtor de Relatórios)
  Os tutoriais do Construtor de Relatórios esperam que você possa exibir e salvar relatórios em um servidor de relatório ou site do SharePoint que esteja integrado com o servidor de relatório. Para dados, todos os tutoriais usam consultas literais que devem ser processadas por uma instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 Se você não tiver acesso a um servidor de relatório, a um site ou a uma fonte de dados, poderá obter informações sobre o Construtor de Relatórios criando um relatório offline. Consulte [Tutorial: Criar um relatório de gráfico rápido offline &#40;Construtor de Relatórios&#41;](report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
## <a name="requirements"></a>Requisitos  
 Você deve ter os seguintes pré-requisitos para concluir os tutoriais do Construtor de Relatórios:  
  
-   Acesso a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Construtor de relatórios. Você pode executar o Construtor de Relatórios usando a versão autônoma do Construtor de Relatórios ou a versão ClickOnce, disponível no Gerenciador de Relatórios ou em um site do SharePoint. Somente a primeira etapa, como abrir o Construtor de Relatórios, é diferente para versões do ClickOnce.  
  
     Para usar Report Manager, abra Report Manager e clique em **Construtor de relatórios**. Por padrão, a URL para Report Manager é http://\<*ServerName*>/Reports.  
  
     Para usar um site do SharePoint, navegue até o site, clique na guia Documentos, clique em Novo Documento e, na lista suspensa, clique em Relatório do Construtor de Relatórios. Por exemplo, http://\<servername>/sites/MySite/Reports. O administrador do SharePoint deve habilitar o recurso Relatório do Construtor de Relatórios para cada biblioteca de documentos.  
  
-   A URL de um servidor de relatório do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] ou de um site do SharePoint integrado a um servidor de relatório do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] . É necessário ter permissão para salvar e exibir relatórios, fontes de dados compartilhadas, conjuntos de dados compartilhados, partes de relatório e modelos. Por padrão, a URL de um servidor de relatório é\<http://servername>/ReportServer. Por padrão, a URL para um site do SharePoint é\<http://sitename> ou\<http://Server>/site.  
  
-   O nome de uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e credenciais suficientes para acesso somente leitura a qualquer banco de dados. As consultas a conjuntos de dados nos tutoriais usam dados literais, mas cada consulta deve ser processada por uma instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] para retornar os metadados necessários a um conjunto de dados de relatório. Por exemplo, a seguinte cadeia de conexão especifica apenas um servidor: `data source=<servername>`. Você deve ter acesso de leitura ao banco de dados padrão atribuído a você pelo administrador do sistema que concede permissão para acessar o servidor. Também é possível especificar um banco de dados, conforme mostrado na seguinte cadeia de conexão: `data source=<servername>;initial catalog=<database>`.  
  
-   Para o tutorial que inclui um mapa, o servidor de relatório deve ser configurado para dar suporte ao Bing Maps como plano de fundo. Para obter mais informações, consulte [planejar o suporte a relatórios de mapa](plan-for-map-report-support.md) na [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] documentação nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [manuais online](https://go.microsoft.com/fwlink/?LinkId=154888) do em msdn.Microsoft.com.  
  
-   O tutorial, [tutorial: Criando relatórios principais e de detalhamento &#40;Construtor de Relatórios&#41;](tutorial-creating-drillthrough-and-main-reports-report-builder.md), usa o conjunto de conjuntos de demonstração contoso Business Intelligence. Esse conjunto de dados é composto do data warehouse ContosoDW e do banco de dados OLAP (processamento analítico online) Contoso_Retail. Os relatórios que você criará neste tutorial recuperam dados do cubo Vendas da Contoso. O banco de dados OLAP Contoso_Retail pode ser baixado no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=18279). Basta baixar o arquivo ContosoBIdemoABF.exe. Ele contém o banco de dados OLAP.  
  
     O outro arquivo, ContosoBIdemoBAK.exe, é para o data warehouse ContosoDW que não é usado neste tutorial.  
  
     O site inclui instruções para extração e restauração do arquivo de backup ContosoRetail.abf no banco de dados OLAP Contoso_Retail.  
  
     Você deve ter acesso a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na qual instalar o banco de dados OLAP.  
  
 O administrador do servidor de relatório deve conceder a você as permissões necessárias no servidor de relatório, configurar os locais das pastas do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] e configurar as opções padrão do Construtor de Relatórios. Para obter mais informações, consulte [instalar, desinstalar e Construtor de relatórios suporte](install-uninstall-and-report-builder-support.md).  
  
## <a name="see-also"></a>Consulte Também  
 [TUTORIAIS &#40;Construtor de Relatórios&#41;](report-builder-tutorials.md)  
  
  
