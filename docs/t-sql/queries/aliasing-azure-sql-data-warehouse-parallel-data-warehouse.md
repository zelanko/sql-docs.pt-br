---
title: Alias (Azure SQL Data Warehouse, Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: "11"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65d5799c33afabe8ebbdb212c13661699b9fea9e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>Alias (Azure SQL Data Warehouse, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Usar alias permite que a substituição temporária de uma cadeia de caracteres curta e fácil de lembrar no lugar de um nome de tabela ou coluna em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] consultas. Aliases de tabela geralmente são usados em consultas de junção, porque a sintaxe de junção requer nomes de objeto totalmente qualificado ao fazer referência a colunas.  
  
 Os aliases devem ser palavras individuais em conformidade com as regras de nomenclatura de objeto. Para obter mais informações, consulte "Regras de nomenclatura de objeto" o [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Aliases não podem conter espaços em branco e não podem ser colocados entre aspas simples ou duplas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_source*  
 O nome da coluna ou tabela de origem.  
  
 AS  
 Preposições um alias opcional. Ao trabalhar com o alias de variável de intervalo, a palavra-chave é proibido.  
  
 *alias*  
 O nome de referência temporário desejado para a tabela ou coluna. Qualquer nome de objeto válido pode ser usado. Para obter mais informações, consulte "Regras de nomenclatura de objeto" o [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir mostra uma consulta com várias junções. Alias de tabela e coluna são demonstradas neste exemplo.  
  
-   Alias de coluna: Ambas as colunas e expressões que envolvem colunas na lista de seleção são um alias neste exemplo. `SalesTerritoryRegion AS SalesTR`Demonstra um alias de coluna simples. `Sum(SalesAmountQuota) AS TotalSales`Demonstra  
  
-   Alias de tabela: `dbo.DimSalesTerritory AS st` mostra a criação do `st` alias para o `dbo.DimSalesTerritory` tabela.  
  
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
  
 A palavra-chave que pode ser excluído, conforme mostrado abaixo, mas geralmente é incluído para fins de legibilidade.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERIR &#40;O Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
