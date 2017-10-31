---
title: SCOPE_IDENTITY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCOPE_IDENTITY
- SCOPE_IDENTITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], SCOPE_IDENTITY function
- SCOPE_IDENTITY function
- last-inserted identity values
- identity values [SQL Server], last-inserted
ms.assetid: eef24670-059b-4f10-91d4-a67bc1ed12ab
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1950d65a35d6fab52025d069e0338493ee7c639d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="scopeidentity-transact-sql"></a>SCOPE_IDENTITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o último valor de identidade inserido em uma coluna de identidade no mesmo escopo. Um escopo é um módulo: um procedimento armazenado, gatilho, função ou lote. Portanto, se duas instruções estarão no mesmo procedimento armazenado, função ou lote, elas estão no mesmo escopo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SCOPE_IDENTITY()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Comentários  
 SCOPE_IDENTITY, IDENT_CURRENT e @@IDENTITY são funções semelhantes porque retornam valores que são inseridos em colunas de identidade.  
  
 IDENT_CURRENT não é limitado por escopo e sessão, mas a uma tabela especificada. IDENT_CURRENT retorna o valor gerado para uma tabela específica em qualquer sessão e escopo. Para obter mais informações, consulte [IDENT_CURRENT &#40; Transact-SQL &#41; ](../../t-sql/functions/ident-current-transact-sql.md).  
  
 SCOPE_IDENTITY e @@IDENTITY retornar o último valor de identidade gerado em qualquer tabela na sessão atual. Entretanto, SCOPE_IDENTITY retorna valores inseridos somente dentro do escopo atual; @@IDENTITY não está limitado a um escopo específico.  
  
 Por exemplo, há duas tabelas, T1 e T2e um gatilho INSERT é definido em T1. Quando uma linha é inserida em T1, o gatilho é acionado e insere uma linha em T2. Esse cenário ilustra dois escopos: a inserção em T1e a inserção em T2 pelo gatilho.  
  
 Supondo que T1 e T2 tenham colunas de identidade, @@IDENTITY e SCOPE_IDENTITY retornam valores diferentes no final de uma instrução INSERT em T1. @@IDENTITY retorna o último valor da coluna de identidade inserido em qualquer escopo na sessão atual. É o valor inserido em T2. SCOPE_IDENTITY () retorna o valor de identidade inserido em T1. Foi a última inserção que ocorreu no mesmo escopo. A função SCOPE_IDENTITY () retorna o valor nulo se a função é invocada antes de qualquer instrução INSERT em uma coluna de identidade ocorrerem no escopo.  
  
 Instruções e transações com falha podem alterar a identidade atual de uma tabela e criar lacunas nos valores da coluna de identidade. O valor de identidade nunca é revertido, mesmo que a transação que tentou inserir o valor na tabela não seja confirmada. Por exemplo, se uma instrução INSERT falhar por causa de uma violação IGNORE_DUP_KEY, o valor de identidade atual para a tabela ainda será incrementado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-identity-and-scopeidentity-with-triggers"></a>A. Usando@IDENTITY e SCOPE_IDENTITY com gatilhos  
 O exemplo a seguir cria duas tabelas, `TZ` e `TY`, e um gatilho INSERT em `TZ`. Quando uma linha é inserida na tabela `TZ`, o gatilho (`Ztrig`) é acionado e insere uma linha em `TY`.  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE TZ (  
   Z_id  int IDENTITY(1,1)PRIMARY KEY,  
   Z_name varchar(20) NOT NULL);  
  
INSERT TZ  
   VALUES ('Lisa'),('Mike'),('Carla');  
  
SELECT * FROM TZ;  
```     
Conjunto de resultados: aparência de tabela TZ.  
  
```  
Z_id   Z_name  
-------------  
1      Lisa  
2      Mike  
3      Carla  
```  
```sql 
CREATE TABLE TY (  
   Y_id  int IDENTITY(100,5)PRIMARY KEY,  
   Y_name varchar(20) NULL);  
  
INSERT TY (Y_name)  
   VALUES ('boathouse'), ('rocks'), ('elevator');  
  
SELECT * FROM TY;  
```   
Conjunto de resultados: aparência TY:  
```  
Y_id  Y_name  
---------------  
100   boathouse  
105   rocks  
110   elevator  
```  

Crie o gatilho que insere uma linha na tabela TY quando uma linha é inserida na tabela TZ.  
```sql  
CREATE TRIGGER Ztrig  
ON TZ  
FOR INSERT AS   
   BEGIN  
   INSERT TY VALUES ('')  
   END;  
```  
ACIONAR o gatilho e determinar quais valores de identidade que você obter com o @@IDENTITY e SCOPE_IDENTITY funções.   
```sql
INSERT TZ VALUES ('Rosalie');  
  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
/*SCOPE_IDENTITY returns the last identity value in the same scope. This was the insert on table TZ.*/`  
SCOPE_IDENTITY  
4  

/*@@IDENTITY returns the last identity value inserted to TY by the trigger. 
  This fired because of an earlier insert on TZ.*/
@@IDENTITY  
115  
```  
  
### <a name="b-using-identity-and-scopeidentity-with-replication"></a>B. Usando@IDENTITY e SCOPE_IDENTITY () com replicação  
 Os exemplos a seguir mostram como usar `@@IDENTITY` e `SCOPE_IDENTITY()` para inserções em um banco de dados publicado para replicação de mesclagem. As duas tabelas dos exemplos estão no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]: `Person.ContactType` não é publicado e `Sales.Customer` é publicado. A replicação de mesclagem adiciona gatilhos a tabelas que são publicadas. Portanto, `@@IDENTITY` pode retornar o valor da inserção em uma tabela do sistema de replicação em vez da inserção em uma tabela de usuário.  
  
 O `Person.ContactType` tabela tem um valor de identidade máximo de 20. Se você inserir uma linha na tabela, `@@IDENTITY` e `SCOPE_IDENTITY()` retornarão o mesmo valor.  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Person.ContactType ([Name]) VALUES ('Assistant to the Manager');  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```  
SCOPE_IDENTITY  
21  
@@IDENTITY  
21
```  
  
 A tabela `Sales.Customer` tem um valor de identidade máximo de 29483. Se você inserir uma linha na tabela, `@@IDENTITY` e `SCOPE_IDENTITY()` retornarão valores diferentes. `SCOPE_IDENTITY()` retorna o valor da inserção em uma tabela de usuário, enquanto `@@IDENTITY` retorna o valor da inserção na tabela do sistema de replicação. Use `SCOPE_IDENTITY()` para aplicativos que requerem acesso ao valor de identidade inserido.  
  
```sql  
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 ```
 SCOPE_IDENTITY  
 29484  
 @@IDENTITY  
 89
 ```  
  
## <a name="see-also"></a>Consulte também  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)  
  
  

