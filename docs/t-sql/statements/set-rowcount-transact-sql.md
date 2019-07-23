---
title: SET ROWCOUNT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_ROWCOUNT_TSQL
- ROWCOUNT_TSQL
- SET ROWCOUNT
- ROWCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- row return limitations [SQL Server]
- SET ROWCOUNT statement
- number of rows affected by statement
- ROWCOUNT option
- counting rows
- stopping queries
- limiting rows returned
- queries [SQL Server], stopping
ms.assetid: c6966fb7-6421-47ef-98f3-82351f2f6bdc
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f79e7931e0e1fd04a699620f65c1dc2566347202
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140227"
---
# <a name="set-rowcount-transact-sql"></a>SET ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Faz o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parar o processamento de consulta depois que o número especificado de linhas for retornado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET ROWCOUNT { number | @number_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 *number* | @*number_var*  
 É o número inteiro de filas a serem processadas antes de finalizar a consulta específica.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  O uso de SET ROWCOUNT não afetará as instruções DELETE, INSERT e UPDATE em uma futura versão do SQL Server. Evite usar SET ROWCOUNT com instruções DELETE, INSERT e UPDATE em um novo trabalho de desenvolvimento e planeje modificar os aplicativos que a utilizam atualmente. Para um comportamento semelhante, use a sintaxe de TOP. Para obter mais informações, confira [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 Para desligar esta opção de forma que todas as linhas sejam retornadas, especifique SET ROWCOUNT 0.  
  
 A configuração da opção SET ROWCOUNT faz com que a maioria das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] parem de processar quando forem afetadas pelo número de linhas especificado. Isso inclui gatilhos. A opção ROWCOUNT não afeta cursores dinâmicos, mas limita o conjunto de linhas de conjunto de chaves e cursores sem distinção. Essa opção deve ser usada com cuidado.  
  
 SET ROWCOUNT substituirá a palavra-chave TOP da instrução SELECT TOP se o número de linhas for o menor valor.  
  
 A configuração de SET ROWCOUNT é definida no momento da execução ou em tempo de execução e não no momento da análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 SET ROWCOUNT para de processar depois do número especificado de linhas. No exemplo a seguir, observe que mais de 500 linhas atendem aos critérios de `Quantity` menor que `300`. Porém, depois de aplicar SET ROWCOUNT, você pode ver que nem todas as linhas foram retornadas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT count(*) AS Count  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Count 
 ----------- 
 537 
 
 (1 row(s) affected)
 ```  
  
 Agora, defina `ROWCOUNT` como `4` e retorne todas as linhas para demonstrar que apenas quatro linhas são retornadas.  
  
```  
SET ROWCOUNT 4;  
SELECT *  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
  
(4 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 SET ROWCOUNT para de processar depois do número especificado de linhas. No exemplo a seguir, observe que mais de 20 linhas atendem aos critérios de `AccountType = 'Assets'`. Porém, depois de aplicar SET ROWCOUNT, você pode ver que nem todas as linhas foram retornadas.  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 5;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
 Para retornar todas as linhas, defina ROWCOUNT como 0.  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 0;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

