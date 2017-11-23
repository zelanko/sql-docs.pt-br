---
title: OPENQUERY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 2a3ad57f9cd898d4c059df725b380be28622035e
ms.contentlocale: pt-br
ms.lasthandoff: 10/02/2017

---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Executa a consulta passagem especificada no servidor vinculado especificado. Esse servidor é uma fonte de dados OLE DB. OPENQUERY pode ser referenciada na cláusula FROM de uma consulta como se fosse um nome de tabela. OPENQUERY também pode ser referenciada como a tabela de destino de uma instrução INSERT, UPDATE ou DELETE. Isso dependerá dos recursos do provedor OLE DB. Embora a consulta possa retornar vários conjuntos de resultados, OPENQUERY retorna somente o primeiro deles.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *linked_server*  
 É um identificador que representa o nome do servidor vinculado.  
  
 **'** *consulta* **'**  
 É a cadeia de caracteres de consulta executada no servidor vinculado. O comprimento máximo da cadeia de caracteres é 8 KB.  
  
## <a name="remarks"></a>Comentários  
 OPENQUERY não aceita variáveis para seus argumentos.  
  
 OPENQUERY não pode ser usado para executar procedimentos armazenados estendidos em um servidor vinculado. Porém, um procedimento armazenado estendido pode ser executado em um servidor vinculado usando um nome de quatro partes. Por exemplo:  
  
```t-sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 Qualquer chamada para OPENDATASOURCE, OPENQUERY ou OPENROWSET na cláusula FROM é avaliada separada e independentemente de qualquer chamada para essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultado da outra.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar OPENQUERY. As permissões que são usadas para conectar ao servidor remoto são obtidas das configurações definidas para o servidor vinculado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. Executando uma consulta de passagem UPDATE  
 O exemplo a seguir usa uma consulta de passagem `UPDATE` no servidor vinculado criado no exemplo A.  
  
```t-sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. Executando uma consulta de passagem INSERT  
 O exemplo a seguir usa uma consulta de passagem `INSERT` no servidor vinculado criado no exemplo A.  
  
```t-sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. Executando um consulta de passagem DELETE  
 O exemplo a seguir usa uma consulta de passagem `DELETE` para excluir a linha inserida no exemplo C.  
  
```t-sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. Executando uma consulta de passagem SELECT  
 O exemplo a seguir usa uma passagem `SELECT` consulta para selecionar a linha inserida no exemplo C.  
  
```t-sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>Consulte também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Funções de conjunto de linhas &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [ONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

