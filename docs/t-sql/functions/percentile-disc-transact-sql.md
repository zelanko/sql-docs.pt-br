---
title: PERCENTILE_DISC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ccd04bec4416fdf5bb5f2137dc2f86e69a9a2ab4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67914340"
---
# <a name="percentile_disc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Computa um percentil específico para obter valores classificados em um conjunto de linhas inteiro ou dentro de partições distintas de um conjunto de linhas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para um determinado valor de percentil *P*, PERCENTILE_DISC classifica os valores de expressão na cláusula ORDER BY. Então ele retorna o valor com o menor valor CUME_DIST fornecido (com relação à mesma especificação de classificação) que é maior ou igual a *P*. Por exemplo, PERCENTILE_DISC (0,5) computará o 50º percentil (ou seja, a mediana) de uma expressão. O PERCENTILE_DISC calcula o percentil com base em uma distribuição discreta dos valores da coluna. O resultado é igual a um valor de coluna específica.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *literal*  
 O percentil a ser computado. O valor deve variar entre 0,0 e 1,0.  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC)**  
 Especifica uma lista de valores sobre os quais classificar e calcular o percentil. Apenas uma *order_by_expression* é permitida. A ordem de classificação padrão é crescente. A lista de valores pode ser de qualquer um dos tipos de dados válidos para a operação de classificação.  
  
 OVER **(** \<partition_by_clause>)**  
 Divide o conjunto de resultados da cláusula FROM em partições. A função de percentil é aplicada nessas partições. Para obter mais informações, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md). A \<cláusula ORDER BY> e a \<cláusula rows ou range> não podem ser especificadas em uma função PERCENTILE_DISC.  
  
## <a name="return-types"></a>Tipos de retorno  
 O tipo de retorno é determinado pelo tipo *order_by_expression*.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
 Sob o nível de compatibilidade 110 e superior, WITHIN GROUP é uma palavra-chave reservada. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 Todos os nulos do conjunto de dados são ignorados.  
  
 PERCENTILE_DISC é não determinística. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="basic-syntax-example"></a>Exemplo de sintaxe básica  

 O exemplo a seguir usa PERCENTILE_CONT e PERCENTILE_DISC para localizar o salário médio dos funcionários de cada departamento. Eles podem não retornar o mesmo valor:
* PERCENTILE_CONT retorna o valor apropriado, mesmo se ele não existir no conjunto de dados.
* PERCENTILE_DISC retorna um valor de conjunto real.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 Este é um conjunto de resultados parcial.  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="basic-syntax-example"></a>Exemplo de sintaxe básica  

 O exemplo a seguir usa PERCENTILE_CONT e PERCENTILE_DISC para localizar o salário médio dos funcionários de cada departamento. Eles podem não retornar o mesmo valor:
* PERCENTILE_CONT retorna o valor apropriado, mesmo se ele não existir no conjunto de dados. 
* PERCENTILE_DISC retorna um valor de conjunto real.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 Este é um conjunto de resultados parcial.  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>Consulte Também  
 [PERCENTILE_CONT &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


