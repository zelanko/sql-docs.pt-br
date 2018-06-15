---
title: Usando aliases (SQL Data Warehouse do Azure, Parallel Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2a44d6a7e2346de0bcfb1d19f0f67fea6049daaa
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33700409"
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>Usando aliases (SQL Data Warehouse do Azure, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  O uso de aliases permite a substituição temporária por uma cadeia de caracteres curta e fácil de lembrar de um nome de tabela ou de coluna em consultas do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)]. Os aliases de tabela geralmente são usados em consultas JOIN, porque a sintaxe de JOIN requer nomes de objeto totalmente qualificados ao referenciar colunas.  
  
 Os aliases precisam ser palavras individuais em conformidade com as regras de nomenclatura de objeto. Para obter mais informações, consulte "Regras de nomenclatura de objeto" em [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Aliases não podem conter espaços em branco e não podem ser colocados entre aspas simples nem duplas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_source*  
 O nome da tabela ou da coluna de origem.  
  
 AS  
 Uma preposição de alias opcional. Ao trabalhar com o uso de alias de variável de intervalo, a palavra-chave AS é proibida.  
  
 *alias*  
 O nome de referência temporário desejado para a tabela ou coluna. Qualquer nome de objeto válido pode ser usado. Para obter mais informações, consulte "Regras de nomenclatura de objeto" em [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir mostra uma consulta com várias junções. O uso de alias de tabela e de coluna é demonstrado neste exemplo.  
  
-   Alias de coluna: as colunas e as expressões que envolvem as colunas na lista de seleção recebem um alias neste exemplo. `SalesTerritoryRegion AS SalesTR` demonstra um alias de coluna simples. `Sum(SalesAmountQuota) AS TotalSales` demonstra  
  
-   Alias de tabela: `dbo.DimSalesTerritory AS st` mostra a criação do alias de `st` para a tabela `dbo.DimSalesTerritory`.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 A palavra-chave AS pode ser excluída, conforme é mostrado abaixo, mas geralmente ela é incluída para facilitar a leitura.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
