---
description: OPENQUERY (Transact-SQL)
title: OPENQUERY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fcabdb207b1e15994323731c30c1a3516222c899
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417212"
---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Executa a consulta passagem especificada no servidor vinculado especificado. Esse servidor é uma fonte de dados OLE DB. OPENQUERY pode ser referenciada na cláusula FROM de uma consulta como se fosse um nome de tabela. OPENQUERY também pode ser referenciada como a tabela de destino de uma instrução INSERT, UPDATE ou DELETE. Isso dependerá dos recursos do provedor OLE DB. Embora a consulta possa retornar vários conjuntos de resultados, OPENQUERY retorna somente o primeiro deles.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *linked_server*  
 É um identificador que representa o nome do servidor vinculado.  
  
 **'** *query* **'**  
 É a cadeia de caracteres de consulta executada no servidor vinculado. O comprimento máximo da cadeia de caracteres é 8 KB.  
  
## <a name="remarks"></a>Comentários  
 OPENQUERY não aceita variáveis para seus argumentos.  
  
 OPENQUERY não pode ser usado para executar procedimentos armazenados estendidos em um servidor vinculado. Porém, um procedimento armazenado estendido pode ser executado em um servidor vinculado usando um nome de quatro partes. Por exemplo:  
  
```sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 Qualquer chamada para OPENDATASOURCE, OPENQUERY ou OPENROWSET na cláusula FROM é avaliada separada e independentemente de qualquer chamada para essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultado da outra.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar OPENQUERY. As permissões que são usadas para conectar ao servidor remoto são obtidas das configurações definidas para o servidor vinculado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-executing-an-update-pass-through-query"></a>a. Executando uma consulta de passagem UPDATE  
 O exemplo a seguir usa uma consulta de passagem `UPDATE` no servidor vinculado criado no exemplo A.  
  
```sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. Executando uma consulta de passagem INSERT  
 O exemplo a seguir usa uma consulta de passagem `INSERT` no servidor vinculado criado no exemplo A.  
  
```sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. Executando um consulta de passagem DELETE  
 O exemplo a seguir usa uma consulta de passagem `DELETE` para excluir a linha inserida no exemplo C.  
  
```sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. Executando uma consulta de passagem SELECT  
 O exemplo a seguir usa uma consulta passagem `SELECT` para excluir a linha inserida no exemplo C.  
  
```sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>Consulte Também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
