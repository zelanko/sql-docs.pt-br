---
title: "Partições habilitadas para gravação | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 82cafa346d2347afa9022a61d9ffce018d9d0dd8
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="partitions---write-enabled-partitions"></a>Partições - partições habilitadas para gravação
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Os dados em um cubo geralmente são somente leitura. Porém, em determinados cenários, você pode desejar que uma partição seja gravada. As partições habilitadas para gravação são usadas para permitir que os usuários empresariais explorem cenários alterando valores de célula e analisando os efeitos das mudanças em dados de cubo. Quando você habilita uma partição para gravação, os aplicativos cliente podem registrar mudanças nos dados da partição. Essas mudanças, conhecidas como dados de write-back, são armazenadas em uma tabela separada e não sobrescrevem quaisquer dados existentes em um grupo de medidas. Porém, elas estarão incorporadas nos resultados de consulta como se elas fizessem parte dos dados de cubo.  
  
 Você pode habilitar um cubo inteiro para gravação, ou apenas determinadas partições do cubo. As dimensões habilitadas para gravação são diferentes, mas complementares. Uma partição habilitada para gravação permite aos usuários atualizarem células da partição, enquanto uma dimensão habilitada para gravação permite aos usuários atualizarem membros de dimensão. Você também pode usar esses dois recursos combinados. Por exemplo, um cubo ou uma partição habilitada para gravação não tem que incluir quaisquer dimensões habilitadas para gravação. **Tópico relacionado:**[Write-Enabled dimensões](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
> [!NOTE]  
>  Para habilitar um cubo para gravação que tem um banco de dados do Microsoft Access como fonte de dados, não use o Microsoft OLE DB Provider for ODBC drivers nas definições de fonte de dados para o cubo, suas partições ou dimensões. Em vez disso, você pode usar o Microsoft Jet 4.0 OLE DB Provider ou qualquer versão do Jet Service Pack que inclua o Jet 4.0 OLE. Para obter mais informações, consulte o artigo da Base de dados de Conhecimento Microsoft [como obter o service pack mais recente para o mecanismo de banco de dados do Microsoft Jet 4.0](http://support.microsoft.com/?kbid=239114).  
  
 Um cubo pode ser habilitada para gravação somente se todas as suas medidas usarem a **soma** função de agregação. Grupos de medidas vinculados e cubos locais não podem ser habilitados para gravação.  
  
## <a name="writeback-storage"></a>Armazenamento de write-back  
 Qualquer alteração feita pelo usuário empresarial será armazenada na tabela de write-back como uma diferença do valor exibido atualmente. Por exemplo, se um usuário final alterar um valor de célula de 90 para 100, o valor **+ 10** é armazenado na tabela de write-back, juntamente com a hora da alteração e obter informações sobre o usuário empresarial que fez. O efeito líquido das alterações acumuladas é exibido nos aplicativos cliente. O valor original no cubo é preservado e uma trilha de auditoria de alterações é registrada na tabela de write-back.  
  
 Alterações em células folha e não folha são tratadas de modo diferente. Uma célula folha representa uma interseção de uma medida e um membro folha de toda dimensão referenciada pelo grupo de medidas. O valor de uma célula folha é obtido diretamente da tabela de fatos e não aceita divisões subsequentes. Se um cubo ou qualquer partição for habilitada para gravação, as alterações poderão ser feitas em uma célula folha. Só poderão ser feitas alterações em uma célula não folha se o aplicativo cliente permitir um modo de distribuir as mudanças entre as células folha que compõem a célula não folha. Esse processo, chamado alocação, é gerenciado pela instrução UPDATE CUBE em linguagens MDX. Os desenvolvedores de business intelligence podem usar a instrução UPDATE CUBE para incluir a funcionalidade de alocação. Para obter mais informações, consulte [instrução UPDATE CUBE &#40; MDX &#41; ](../../mdx/mdx-data-manipulation-update-cube.md).  
  
> [!IMPORTANT]  
>  Quando células atualizadas não se sobrepõem, a propriedade de cadeia de conexão **Atualizar Nível de Isolamento** pode ser usada para aprimorar o desempenho de UPDATE CUBE. Para obter mais informações, consulte <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
 Independentemente de um aplicativo cliente distribuir alterações feitas em células não folha, na avaliação das consultas, são feitas mudanças na tabela de write-back em células folha e não folha, para que usuários empresariais possam visualizar os efeitos das mudanças ao longo do cubo.  
  
 Alterações feitas pelo usuário empresarial são mantidas em uma tabela de write-back separada com a qual você pode trabalhar da seguinte maneira:  
  
-   Converter em uma partição para incorporar alterações no cubo permanentemente. Essa ação torna o grupo de medidas somente leitura. Você pode especificar uma expressão de filtro para selecionar as mudanças que deseja converter.  
  
-   Descartar para retornar a partição a seu estado original. Essa ação torna a partição de medidas somente leitura.  
  
## <a name="security"></a>Segurança  
 Um usuário empresarial tem permissão para registrar mudanças na tabela de write-back de um cubo apenas se pertencer a uma função que tenha permissão de leitura/gravação em células do cubo. Para cada função, você pode controlar quais células do cubo podem ou não ser atualizadas. Para obter mais informações, consulte [conceder ao cubo ou permissões de modelo &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões habilitadas para gravação](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [Agregações e Designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Partições &#40; Analysis Services - dados multidimensionais &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Dimensões habilitadas para gravação](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
