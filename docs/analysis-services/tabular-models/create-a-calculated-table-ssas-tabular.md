---
title: Criar uma tabela calculada (SSAS Tabular) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7ff98a-82a9-4333-a7d3-7a95a6f2caf7
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e7db92207b2a518c3d697b997a22ed7c076cd0b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-calculated-table-ssas-tabular"></a>Criar uma tabela calculada (SSAS tabular)
  Um *tabela calculada* é um objeto computado baseado em uma expressão ou consulta DAX, derivado do todo ou de parte de outras tabelas no mesmo modelo.  
  
 Um problema de design comum que as tabelas calculadas podem resolver é ter uma interface com uma dimensão com função múltipla em um contexto específico para que você possa expô-la como uma estrutura de consulta em aplicativos cliente.  Você deve se lembrar que uma dimensão com função múltipla é simplesmente uma tabela com interface em vários contextos — um exemplo clássico é a tabela Data, incluída no manifesto como OrderDate, ShipDate ou DueDate, dependendo da relação de chave estrangeira. Ao criar uma tabela calculada para ShipDate explicitamente, você obtém uma tabela autônoma que é disponibilizada para consultas, tão completamente operável quanto qualquer outra tabela.  
  
 Um segundo uso de uma tabela calculada inclui configurar um conjunto de linhas filtradas ou um subconjunto ou superconjunto de colunas de outras tabelas existentes. Isso permite manter a tabela original intacta enquanto você cria variações dessa tabela para dar suporte a cenários específicos.  
  
 Usar tabelas calculadas para obter as melhores vantagens exigirá que você saiba pelo menos um pouco de DAX. À medida que você trabalha com expressões em sua tabela, pode ser útil saber que uma tabela calculada contém uma única partição com um DAXSource, em que a expressão é uma expressão DAX.  
Há uma CalculatedTableColumn para cada coluna retornada pela expressão, em que SourceColumn é o nome da coluna retornada (semelhante a DataColumns em tabelas não calculadas).  
  
## <a name="how-to-create-a-calculated-table"></a>Como criar uma tabela calculada  
  
1.  Primeiro, verifique se que o modelo de tabela tem um nível de compatibilidade de 1200 ou superior. Você pode verificar a propriedade **Nível de Compatibilidade** no modelo no SSDT.  
  
2.  Alterne para a Exibição de Dados. Você não pode criar uma tabela calculada na Exibição de Diagrama.  
  
3.  Selecione **Tabela** > **Nova tabela calculada**.  
  
4.  Digite ou cole uma expressão DAX (veja abaixo algumas ideias).  
  
5.  Dê um nome para a tabela.  
  
6.  Crie relações com outras tabelas no modelo. Consulte [Criar uma relação entre duas tabelas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md) se você precisar de ajuda com esta etapa.  
  
7.  Faça referência à tabela em cálculos ou expressões no seu modelo ou use **Analisar no Excel** para exploração de dados ad hoc.  
  
### <a name="replicate-a-role-playing-dimension"></a>Replicar uma dimensão com função múltipla  
 Na barra de fórmulas, digite uma fórmula DAX que obtém uma cópia de outra tabela. Depois que a tabela calculada for populada, dê a ela um nome descritivo e configure uma relação que use a chave estrangeira específica à função. Por exemplo, no banco de dados Adventure Works, você pode criar uma tabela calculada para Data de Vencimento e usar DueDateKey como a base de uma relação com a tabela de fatos.  
  
```  
=DimDate  
```  
  
### <a name="summarized-or-filtered-dataset"></a>Conjunto de dados resumido ou filtrado  
 Na barra de fórmulas, digite uma expressão DAX que filtre, resuma ou, de alguma forma, manipule um conjunto de dados para conter as linhas desejadas. Esse exemplo agrupa por vendas, cor e moeda.  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### <a name="superset-using-columns-from-multiple-tables"></a>Superconjunto usando colunas de várias tabelas  
 Na barra de fórmulas, digite uma expressão DAX que combine colunas de várias tabelas. Nesse caso, a saída da consulta lista a categoria de produto para cada moeda.  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Expressões de análise de dados &#40; DAX &#41; no Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [Noções básicas sobre DAX em modelos de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  

