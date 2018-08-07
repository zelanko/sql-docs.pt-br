---
title: USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- USER
- USER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- system-supplied usernames [SQL Server]
- USER function
- users [SQL Server], database names
- names [SQL Server], database users
- database usernames [SQL Server]
ms.assetid: 82bbbd94-870c-4c43-9ed9-d9abc767a6be
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e51ea87446661c20e2af58a79daec00f091a0ad2
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453244"
---
# <a name="user-transact-sql"></a>USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Permite um valor fornecido pelo sistema para o nome de usuário de banco de dados do usuário atual a ser inserido em uma tabela quando nenhum valor padrão é especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
USER  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **char**  
  
## <a name="remarks"></a>Remarks  
 USER fornece a mesma funcionalidade como a função de sistema USER_NAME.  
  
 Use USER com restrições DEFAULT nas instruções CREATE TABLE ou ALTER TABLE, ou use como qualquer função padrão.  
  
 USER sempre retorna o nome do contexto atual. Quando chamado depois de uma instrução EXECUTE AS, USER retorna o nome do contexto representado.  
  
 Se um principal do Windows acessar o banco de dados específico por meio da associação em um grupo, USER retornará o principal do Windows em vez do nome do grupo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-user-to-return-the-database-user-name"></a>A. Usando USER para retornar o nome do usuário do banco de dados  
 O exemplo a seguir declara uma variável como `char`, atribui o valor atual de USER a ela e imprime a variável com uma descrição de texto.  
  
```  
DECLARE @usr char(30)  
SET @usr = user  
SELECT 'The current user''s database username is: '+ @usr  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-----------------------------------------------------------------------  
The current user's database username is: dbo  
  
(1 row(s) affected)
```  
  
### <a name="b-using-user-with-default-constraints"></a>B. Usando USER com restrições DEFAULT  
 O exemplo a seguir cria uma tabela usando `USER` como uma restrição `DEFAULT` para o vendedor de uma linha de vendas.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE inventory22  
(  
 part_id int IDENTITY(100, 1) NOT NULL,  
 description varchar(30) NOT NULL,  
 entry_person varchar(30) NOT NULL DEFAULT USER   
)  
GO  
INSERT inventory22 (description)  
VALUES ('Red pencil')  
INSERT inventory22 (description)  
VALUES ('Blue pencil')  
INSERT inventory22 (description)  
VALUES ('Green pencil')  
INSERT inventory22 (description)  
VALUES ('Black pencil')  
INSERT inventory22 (description)  
VALUES ('Yellow pencil')  
GO  
```  
  
 Esta é a consulta para selecionar todas as informações da tabela `inventory22`:  
  
```  
SELECT * FROM inventory22 ORDER BY part_id;  
GO  
```  
  
 Este é o conjunto de resultados (observe o valor `entry-person`):  
  
 ```
part_id     description                    entry_person
----------- ------------------------------ -------------------------
100         Red pencil                     dbo
101         Blue pencil                    dbo
102         Green pencil                   dbo
103         Black pencil                   dbo
104         Yellow pencil                  dbo
  
(5 row(s) affected)
```  
  
### <a name="c-using-user-in-combination-with-execute-as"></a>C. Usando USER em combinação com EXECUTE AS  
 O exemplo a seguir ilustra o comportamento de `USER` quando chamado em uma sessão representada.  
  
```  
SELECT USER;  
GO  
EXECUTE AS USER = 'Mario';  
GO  
SELECT USER;  
GO  
REVERT;  
GO  
SELECT USER;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO
Mario
DBO
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)  
  
  

