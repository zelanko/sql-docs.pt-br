---
title: Partições habilitadas para gravação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13864dba5cac0274204050a8c78730de29f3321e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727170"
---
# <a name="write-enabled-partitions"></a>Partições habilitadas para gravação
  Os dados em um cubo geralmente são somente leitura. Porém, em determinados cenários, você pode desejar que uma partição seja gravada. As partições habilitadas para gravação são usadas para permitir que os usuários empresariais explorem cenários alterando valores de célula e analisando os efeitos das mudanças em dados de cubo. Quando você habilita uma partição para gravação, os aplicativos cliente podem registrar mudanças nos dados da partição. Essas mudanças, conhecidas como dados de write-back, são armazenadas em uma tabela separada e não sobrescrevem quaisquer dados existentes em um grupo de medidas. Porém, elas estarão incorporadas nos resultados de consulta como se elas fizessem parte dos dados de cubo.  
  
 Você pode habilitar um cubo inteiro para gravação, ou apenas determinadas partições do cubo. As dimensões habilitadas para gravação são diferentes, mas complementares. Uma partição habilitada para gravação permite aos usuários atualizarem células da partição, enquanto uma dimensão habilitada para gravação permite aos usuários atualizarem membros de dimensão. Você também pode usar esses dois recursos combinados. Por exemplo, um cubo ou uma partição habilitada para gravação não tem que incluir quaisquer dimensões habilitadas para gravação. **Tópico relacionado:**[dimensões habilitadas para gravação](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
> [!NOTE]  
>  Para habilitar um cubo para gravação que tem um banco de dados do Microsoft Access como fonte de dados, não use o Microsoft OLE DB Provider for ODBC drivers nas definições de fonte de dados para o cubo, suas partições ou dimensões. Em vez disso, você pode usar o Microsoft Jet 4.0 OLE DB Provider ou qualquer versão do Jet Service Pack que inclua o Jet 4.0 OLE. Para obter mais informações, consulte o artigo da base de dados de conhecimento Microsoft sobre [como obter as Service Pack mais recentes para o Microsoft Jet 4,0 mecanismo de banco de dados](https://support.microsoft.com/?kbid=239114).  
  
 Um cubo só poderá ser habilitado para gravação se todas as suas medidas usarem a função de agregação `Sum`. Grupos de medidas vinculados e cubos locais não podem ser habilitados para gravação.  
  
## <a name="writeback-storage"></a>Armazenamento de write-back  
 Qualquer alteração feita pelo usuário empresarial será armazenada na tabela de write-back como uma diferença do valor exibido atualmente. Por exemplo, se um usuário final alterar um valor de célula de 90 para 100, o valor `+10` será armazenado na tabela de write-back, juntamente com a hora da mudança e as informações sobre o usuário empresarial que fez a alteração. O efeito líquido das alterações acumuladas é exibido nos aplicativos cliente. O valor original no cubo é preservado e uma trilha de auditoria de alterações é registrada na tabela de write-back.  
  
 Alterações em células folha e não folha são tratadas de modo diferente. Uma célula folha representa uma interseção de uma medida e um membro folha de toda dimensão referenciada pelo grupo de medidas. O valor de uma célula folha é obtido diretamente da tabela de fatos e não aceita divisões subsequentes. Se um cubo ou qualquer partição for habilitada para gravação, as alterações poderão ser feitas em uma célula folha. Só poderão ser feitas alterações em uma célula não folha se o aplicativo cliente permitir um modo de distribuir as mudanças entre as células folha que compõem a célula não folha. Esse processo, chamado alocação, é gerenciado pela instrução UPDATE CUBE em linguagens MDX. Os desenvolvedores de business intelligence podem usar a instrução UPDATE CUBE para incluir a funcionalidade de alocação. Para obter mais informações, consulte a [instrução UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
> [!IMPORTANT]  
>  Quando células atualizadas não se sobrepõem, a propriedade de cadeia de caracteres da conexão `Update Isolation Level` pode ser usada para aprimorar o desempenho de UPDATE CUBE. Para obter mais informações, consulte <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
 Independentemente de um aplicativo cliente distribuir alterações feitas em células não folha, na avaliação das consultas, são feitas mudanças na tabela de write-back em células folha e não folha, para que usuários empresariais possam visualizar os efeitos das mudanças ao longo do cubo.  
  
 Alterações feitas pelo usuário empresarial são mantidas em uma tabela de write-back separada com a qual você pode trabalhar da seguinte maneira:  
  
-   Converter em uma partição para incorporar alterações no cubo permanentemente. Essa ação torna o grupo de medidas somente leitura. Você pode especificar uma expressão de filtro para selecionar as mudanças que deseja converter.  
  
-   Descartar para retornar a partição a seu estado original. Essa ação torna a partição de medidas somente leitura.  
  
## <a name="security"></a>Segurança  
 Um usuário empresarial tem permissão para registrar mudanças na tabela de write-back de um cubo apenas se pertencer a uma função que tenha permissão de leitura/gravação em células do cubo. Para cada função, você pode controlar quais células do cubo podem ou não ser atualizadas. Para obter mais informações, consulte [conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Dimensões habilitadas para gravação](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [Agregações e designs de agregação](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Partições &#40;Analysis Services de dados multidimensionais&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Dimensões habilitadas para gravação](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
