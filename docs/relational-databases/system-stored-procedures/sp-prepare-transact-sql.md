---
title: sp_prepare (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b52f71577bed8a0433c8d516cdc9cbd877066e4
ms.sourcegitcommit: f46fd79fd32a894c8174a5cb246d9d34db75e5df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/26/2018
ms.locfileid: "53785927"
---
# <a name="spprepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Prepara um parametrizada [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução e retorna uma instrução *manipular* para execução.  `sp_prepare` é invocado pela especificação de ID = 11 em um pacote do protocolo TDS.  
  
 ![Ícone do link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone do link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador*  
 É gerado um SQL Server *identificador preparado* identificador. *manipular* é um parâmetro obrigatório com um **int** valor de retorno.  
  
 *params*  
 Identifica instruções parametrizadas. O *params* definição de variáveis é substituída para marcadores de parâmetro na instrução. *params* é um parâmetro obrigatório que chama uma **ntext**, **nchar**, ou **nvarchar** valor de entrada. Insira um valor NULL se a instrução não for parametrizada.  
  
 *stmt*  
 Define o conjunto de resultados do cursor. O *stmt* parâmetro é obrigatório e chamadas para um **ntext**, **nchar**, ou **nvarchar** valor de entrada.  
  
 *Opções*  
 Um parâmetro opcional que retorna uma descrição das colunas do conjunto de resultados de cursor. *opções* requer o seguinte valor de entrada de int:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>Exemplos  
A. O exemplo a seguir prepara e executa uma instrução simples.  
  
```sql  
DECLARE @P1 int;  
EXEC sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
EXEC sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```

b. O exemplo a seguir prepara uma instrução no banco de dados AdventureWorks2016 e, posteriormente, executa-o usando o identificador.

```sql
-- Prepare query
DECLARE @P1 int;  
EXEC sp_prepare @P1 output,   
    N'@Param int',  
    N'SELECT *
FROM Sales.SalesOrderDetail AS sod
INNER JOIN Production.Product AS p ON sod.ProductID = p.ProductID
WHERE SalesOrderID = @Param
ORDER BY Style DESC;';  

-- Return handle for calling application
SELECT @P1;
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
-----------
1

(1 row affected)
```

Em seguida, o aplicativo executa a consulta usando duas vezes o valor do identificador 1, antes de descartar o plano preparado.

```sql
EXEC sp_execute 1, 49879;  
GO

EXEC sp_execute 1, 48766;
GO

EXEC sp_unprepare 1; 
GO
```
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  

