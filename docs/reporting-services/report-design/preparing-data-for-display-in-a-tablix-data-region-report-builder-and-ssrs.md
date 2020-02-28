---
title: Como preparar dados para exibição em uma região de dados Tablix (Construtor de Relatórios) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: fbb00dc6-7887-480c-b771-cab6fecb8dcc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf1e776b874a371dceeef8c10306a55efdd1a2ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77082404"
---
# <a name="preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs"></a>Preparando dados para exibição em uma região de dados Tablix (Construtor de Relatórios e SSRS)
  Uma região de dados tablix exibe dados de um conjunto de dados. É possível exibir todos os dados recuperados do conjunto de dados ou criar filtros para exibir apenas um subconjunto dos dados. Você também pode adicionar expressões condicionais para preencher valores nulos ou modificar a consulta de um conjunto de dados para incluir colunas que identificam a ordem de classificação de uma coluna existente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="working-with-nulls-and-blanks-in-field-values"></a>Trabalhando com nulos e espaços em branco em valores de campo  
 Entre os dados da coleção de campos em um conjunto de dados estão todos os valores recuperados da fonte de dados em tempo de execução, inclusive valores nulos e espaços em branco. Valores nulos e espaços em branco costumam ser indistinguíveis. Na maioria dos casos, trata-se do comportamento desejado. Por exemplo, funções de agregação numéricas como [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) e [Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md) ignoram valores nulos. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
 Caso você queira tratar valores nulos de maneira diferente, é possível usar expressões condicionais ou o código personalizado para substituir um valor personalizado do valor nulo. Por exemplo, a seguinte expressão substitui o texto `Null` independentemente de onde o valor nulo ocorra no campo `[Size]`.  
  
```  
=IIF(Fields!Size.Value IS NOTHING,"Null",Fields!Size.Value)  
```  
  
 Para obter mais informações sobre como eliminar nulos nos dados antes de recuperar dados de uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando consultas [!INCLUDE[tsql](../../includes/tsql-md.md)], veja [NULL e UNKNOWN (Transact-SQL)](../../t-sql/language-elements/null-and-unknown-transact-sql.md).  
  
## <a name="handling-null-field-names"></a>Tratando nomes de campo nulos  
 Não há problemas em testar valores nulos em uma expressão contanto que o próprio campo esteja no conjunto de resultados da consulta. Usando código personalizado, é possível testar se o próprio campo está presente nos campos da coleção retornados da fonte de dados em tempo de execução. Para obter mais informações, consulte [Referências de coleções de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).  
  
## <a name="adding-a-sort-order-column"></a>Adicionando uma coluna de ordem de classificação  
 Por padrão, é possível classificar valores de um campo de conjunto de dados por ordem alfabética. Para classificar em uma ordem diferente, é possível adicionar uma nova coluna ao conjunto de dados que define a ordem de classificação desejada em uma região de dados. Por exemplo, para classificar o campo `[Color]` e os itens branco e preto primeiro, é possível adicionar uma coluna `[ColorSortOrder]`, mostrada na seguinte consulta:  
  
```  
SELECT ProductID, p.Name, Color,  
   CASE  
      WHEN p.Color = 'White' THEN 1  
      WHEN p.Color = 'Black' THEN 2  
      WHEN p.Color = 'Blue' THEN 3  
      WHEN p.Color = 'Yellow' THEN 4  
      ELSE 5  
   END As ColorSortOrder  
FROM Production.Product p  
```  
  
 Para classificar uma região de dados de tabela de acordo com essa ordem de classificação, defina a expressão de classificação no grupo detalhado como `=Fields!ColorSortOrder.Value`. Para obter mais informações, consulte [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
