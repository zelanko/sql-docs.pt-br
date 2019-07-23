---
title: CURSOR_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURSOR_STATUS
- CURSOR_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], cursors
- CURSOR_STATUS function
- cursors [SQL Server], status information
ms.assetid: 3a4a840e-04f8-43bd-aada-35d78c3cb6b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 892e4c09154e93ded7718819c86dfe91c18c85ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026255"
---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Para determinado parâmetro, `CURSOR_STATUS` mostra se uma declaração de cursor retornou ou não um cursor e conjunto de resultados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CURSOR_STATUS   
     (  
          { 'local' , 'cursor_name' }   
          | { 'global' , 'cursor_name' }   
          | { 'variable' , 'cursor_variable' }   
     )  
```  
  
## <a name="arguments"></a>Argumentos  
'local'  
Especifica uma constante indicando que a fonte do cursor é um nome de cursor local.
  
'*cursor_name*'  
É o nome do cursor. Um nome de cursor deve estar em conformidade com as [regras do identificador do banco de dados](../../relational-databases/databases/database-identifiers.md).
  
'global'  
Especifica uma constante indicando que a fonte do cursor é um nome de cursor global.
  
'variável'  
Especifica uma constante indicando que a fonte do cursor é uma variável local.
  
'*cursor_variable*'  
É o nome da variável de cursor. Uma variável de cursor deve ser definida usando o tipo de dados **cursor**.
  
## <a name="return-types"></a>Tipos de retorno
**smallint**
  
|Valor retornado|Cursor name|Variável de cursor|  
|---|---|---|
|1|O conjunto de resultados do cursor tem, ao menos, uma linha.<br /><br /> Para cursores insensitive e keyset, o conjunto de resultados terá ao menos uma linha.<br /><br /> Para cursores dinâmicos, o conjunto de resultados pode ter zero, uma ou mais linhas.|O cursor alocado a esta variável está aberto.<br /><br /> Para cursores insensitive e keyset, o conjunto de resultados terá ao menos uma linha.<br /><br /> Para cursores dinâmicos, o conjunto de resultados pode ter zero, uma ou mais linhas.|  
|0|O conjunto de resultados do cursor está vazio.*|O cursor alocado a esta variável está aberto, mas o conjunto de resultados está definitivamente vazio.*|  
|-1|O cursor está fechado.|O cursor alocado a esta variável está fechado.|  
|-2|Não aplicável.|Tem uma destas possibilidades:<br /><br /> O procedimento chamado anteriormente não atribuiu um cursor a essa variável OUTPUT.<br /><br /> O procedimento atribuído previamente atribuiu um cursor a essa variável OUTPUT, mas o cursor estava em estado de fechamento na conclusão do procedimento. Portanto, o cursor é desalocado, e não é retornado ao procedimento de chamada.<br /><br /> Nenhum cursor é atribuído à variável de cursor declarada.|  
|-3|Um cursor com o nome especificado não existe.|Uma variável de cursor com o nome especificado não existe ou, se existe, nenhum cursor foi alocado a ela ainda.|  
  
*Cursores dinâmicos nunca retornam esse resultado.
  
## <a name="examples"></a>Exemplos  
Este exemplo usa a função `CURSOR_STATUS` para mostrar o status de um cursor, após sua declaração, depois que ele é aberto e depois que é fechado.
  
```sql
CREATE TABLE #TMP  
(  
   ii int  
)  
GO  
  
INSERT INTO #TMP(ii) VALUES(1)  
INSERT INTO #TMP(ii) VALUES(2)  
INSERT INTO #TMP(ii) VALUES(3)  
  
GO  
  
--Create a cursor.  
DECLARE cur CURSOR  
FOR SELECT * FROM #TMP  
  
--Display the status of the cursor before and after opening  
--closing the cursor.  
  
SELECT CURSOR_STATUS('global','cur') AS 'After declare'  
OPEN cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Open'  
CLOSE cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Close'  
  
--Remove the cursor.  
DEALLOCATE cur  
  
--Drop the table.  
DROP TABLE #TMP  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
After declare
---------------
-1  
  
After Open
----------
1  
  
After Close
-----------
-1
```  
  
## <a name="see-also"></a>Confira também
[Funções do cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
