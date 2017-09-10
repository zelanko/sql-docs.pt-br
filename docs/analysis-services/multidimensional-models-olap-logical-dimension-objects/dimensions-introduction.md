---
title: "Noções básicas sobre dimensões (Analysis Services - dados multidimensionais) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9320eebfc25964e5e751e2d93ffc8cb7503861e5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions---introduction"></a>Dimensões - Introdução
  A Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dimensões são grupos de atributos com base nas colunas de tabelas ou exibições em uma exibição da fonte de dados. As dimensões existem independentes de um cubo, podem ser usadas em vários cubos, podem ser usadas várias vezes em um único cubo e estarem vinculadas entre instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma dimensão que existe, independentemente de um cubo, é chamada de dimensão de banco de dados e uma instância de uma dimensão de banco de dados dentro de um cubo é chamada de dimensão do cubo.  
  
## <a name="dimension-based-on-a-star-schema-design"></a>Dimensão com base em Design de esquema em estrela  
 A estrutura de uma dimensão é amplamente direcionada pela estrutura da tabela ou tabelas de dimensões subjacentes. A estrutura mais simples é chamada de esquema em estrela, onde cada dimensão com base em uma única tabela de dimensões diretamente vinculada à tabela de fatos por uma relação chave primária-chave estrangeira.  
  
 O diagrama a seguir ilustra a subseção do [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] banco de dados de exemplo, no qual o **FactResellerSales** tabela de fatos é relacionada a duas tabelas de dimensão, **DimReseller** e **DimPromotion**. O **ResellerKey** coluna o **FactResellerSales** tabela de fatos define uma relação de chave estrangeira para a **ResellerKey** coluna de chave primária no  **DimReseller** tabela de dimensões. Da mesma forma, o **PromotionKey** coluna o **FactResellerSales** tabela de fatos define uma relação de chave estrangeira para a **PromotionKey** coluna de chave primária no  **DimPromotion** tabela de dimensões.  
  
 ![Esquema lógico para relação de dimensão de fatos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimfactrelationship.gif "esquema lógico para relação de dimensão de fatos")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>Dimensão com base em Design de esquema floco de neve   
 Frequentemente, uma estrutura mais complexa é necessária, pois são necessárias informações de várias tabelas para definir a dimensão. Nessa estrutura, chamada de esquema floco de neve, cada dimensão com base em atributos de colunas em várias tabelas vinculadas umas às outras e, finalmente, à tabela de fatos pela relação chave primária-chave estrangeira. Por exemplo, o diagrama a seguir ilustra as tabelas necessárias para descrever completamente a dimensão produto no **AdventureWorksDW** projeto de exemplo:  
  
 ![Tabelas de dimensão AdventureWorksAS Product](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimproduct.gif "tabelas de dimensão AdventureWorksAS Product")  
  
 Para descrever completamente um produto, a categoria subcategoria do produto deve ser incluída na dimensão Produto. No entanto, essas informações não residem diretamente na tabela principal para o **DimProduct** dimensão. Uma relação de chave estrangeira de **DimProduct** para **DimProductSubcategory**, que por sua vez tem uma relação de chave estrangeira para a **DimProductCategory** da tabela, torna é possível incluir as informações de produto categorias e subcategorias na dimensão produto.  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>Esquema floco de neve versus relação de referência  
 Algumas vezes, você pode ter que fazer uma escolha entre usar um esquema floco de neve para definir atributos em uma dimensão de várias tabelas ou definir duas dimensões separadas e definir uma relação de dimensão de referência entre elas: O diagrama a seguir ilustra esse cenário.  
  
 ![Esquema lógico para dimensão referenciada de exemplo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/dimindirect.gif "esquema lógico para dimensão referenciada de exemplo")  
  
 No diagrama anterior, o **FactResellerSales** tabela de fatos não tem uma relação de chave estrangeira com a **DimGeography** tabela de dimensões. No entanto, o **FactResellerSales** tabela de fatos tem uma relação de chave estrangeira com a **DimReseller** tabela de dimensão, que por sua vez, tem uma relação de chave estrangeira com a  **DimGeography** tabela de dimensões. Para definir a dimensão revendedor que contém informações geográficas sobre cada revendedor, você precisa recuperar esses atributos do **DimGeography** e **DimReseller** tabelas de dimensões. No entanto, em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você obter o mesmo resultado criando duas dimensões separadas e vinculando-as em um grupo de medidas definindo uma relação de dimensão de referência entre as duas dimensões. Para obter mais informações sobre relações de dimensão de referência, consulte [relações de dimensão](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Uma vantagem de usar as relações de dimensão de referência nesse cenário é que, você pode criar uma única dimensão geográfica e, depois, criar várias dimensões de cubo com base na dimensão geográfica, sem necessitar de qualquer espaço de armazenamento adicional. Por exemplo, você pode vincular uma das dimensões geográficas do cubo a uma dimensão de revendedor e outra dimensão geográfica do cubo à dimensão de cliente. **Tópicos relacionados:**[relações de dimensão](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md), [definir uma relação referenciada e propriedades de relação referenciada](../../analysis-services/multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>Processando uma dimensão  
 Depois de criar uma dimensão, você deve processá-la antes de visualizar um os membros de atributos e hierarquias na dimensão. Depois que a estrutura da dimensão mudar ou as informações nas tabelas subjacentes forem atualizadas, você precisará processar a dimensão novamente antes de exibir as alterações. Ao processar uma dimensão após as alterações estruturais, você deve também processar os cubos que incluem a dimensão — ou o cubo não será exibível.  
  
## <a name="security"></a>Segurança  
 Todos os objetos subordinados da dimensão, incluindo hierarquias, níveis e membros são protegidos por meio das funções no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A segurança de dimensão pode ser aplicada para todos os cubos no banco de dados que usa a dimensão ou por apenas um cubo específico. Para obter mais informações sobre a segurança de dimensão, consulte [conceder permissões em uma dimensão &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Armazenamento de dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [Conversões de dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Dimensões habilitadas para gravação](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
