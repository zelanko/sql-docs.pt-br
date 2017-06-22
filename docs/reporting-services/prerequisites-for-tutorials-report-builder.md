---
title: "Pré-requisitos para tutoriais (construtor de relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2c2056dccbb2d65e880928e4ec37a70080cfbf53
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="prerequisites-for-tutorials-report-builder"></a>Pré-requisitos para tutoriais (Construtor de Relatórios)

Para realizar os tutoriais do Construtor de Relatórios, você precisa conseguir exibir e salvar relatórios paginados do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] em um servidor de relatório ou site do SharePoint integrado a um servidor de relatório. Para dados, todos os tutoriais usam consultas literais que devem ser processadas por uma instância do SQL Server.  
  
Se você não tiver acesso a um servidor de relatório, a um site ou a uma fonte de dados, poderá obter informações sobre o Construtor de Relatórios criando um relatório offline. Consulte [Tutorial: Criar um relatório de gráfico rápido offline &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  

## <a name="requirements"></a>Requisitos

Você deve ter os seguintes pré-requisitos para concluir os tutoriais do Construtor de Relatórios:  
  
-   Acesso ao construtor de relatórios. Você pode executar o Construtor de Relatórios em um servidor de relatório do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] no modo integrado do SharePoint. Somente a primeira etapa, como abrir o Construtor de Relatórios, é diferente nos servidores diferentes.  
  
    Em um servidor de relatório, selecione **Novo** > **Relatório Paginado**.
  
    Em um servidor de relatório no modo integrado do SharePoint, na guia **Documentos** , selecione **Novo Documento**e, na lista suspensa, selecione **Relatório do Construtor de Relatórios**. Por exemplo, `http://<servername>/sites/mySite/reports`. O administrador do SharePoint deve habilitar o recurso Relatório do Construtor de Relatórios para cada biblioteca de documentos.  
  
-   A URL de um servidor de relatório do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou de um site do SharePoint integrado a um servidor de relatório do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . É necessário ter permissão para salvar e exibir relatórios, fontes de dados compartilhadas, conjuntos de dados compartilhados, partes de relatório e modelos. Por padrão, a URL de um servidor de relatório é `http://<servername>/reportserver`. Por padrão, a URL de um site do SharePoint é `http://<sitename>` ou `http://<server>/site`.  
  
-   O nome de uma instância do SQL Server e credenciais suficientes para acesso somente leitura a qualquer banco de dados. As consultas de conjunto de dados nos tutoriais usam dados literais, mas cada consulta deve ser processada por uma instância do SQL Server para retornar os metadados que é necessário para um conjunto de dados do relatório. Por exemplo, a seguinte cadeia de conexão especifica apenas um servidor: `data source=<servername>`. Você deve ter acesso de leitura ao banco de dados padrão atribuído a você pelo administrador do sistema que concede permissão para acessar o servidor. Também é possível especificar um banco de dados, conforme mostrado na seguinte cadeia de conexão: `data source=<servername>;initial catalog=<database>`.  
  
-   Para o [Tutorial: relatório de mapa (construtor de relatórios)](Tutorial:%20Map%20Report%20\(Report%20Builder\).md), o servidor de relatório deve estar configurado para suportar o Bing maps como plano de fundo. Para obter mais informações, consulte [Planejar suporte ao relatório de mapa](http://msdn.microsoft.com/en-us/5ddc97a7-7ee5-475d-bc49-3b814dce7e19).   

-   O [Tutorial: Criando detalhamento e principal relatórios (construtor de relatórios)](Tutorial:%20Creating%20Drillthrough%20and%20Main%20Reports%20\(Report%20Builder\).md) tutorial exige acesso ao cubo vendas da Contoso. Consulte o tutorial para obter mais informações. 
  
O administrador do servidor de relatório deve conceder a você as permissões necessárias no servidor de relatório, configurar os locais das pastas do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] e configurar as opções padrão do Construtor de Relatórios. Para obter mais informações, consulte [Instalar e desinstalar o Construtor de Relatórios](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416).  

## <a name="next-steps"></a>Próximas etapas

[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
