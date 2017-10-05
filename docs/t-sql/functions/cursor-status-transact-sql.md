---
title: CURSOR_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e88dd4f14d8bd6fc90c40df101bfd9b2895bf229
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Uma função escalar que permite o chamador de um procedimento armazenado para determinar se o procedimento retornou um cursor e conjunto de resultados para um determinado parâmetro ou não.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
Especifica uma constante que indica a fonte do cursor é um nome de cursor local.
  
'*cursor_name*'  
É o nome do cursor. Um nome de cursor deve obedecer às regras para identificadores.
  
'global'  
Especifica uma constante que indica que a fonte do cursor é um nome de cursor global.
  
'variável'  
Especifica uma constante que indica que a fonte do cursor é uma variável local.
  
'*cursor_variable*'  
É o nome do cursor variável. Uma variável de cursor deve ser definida usando o **cursor** tipo de dados.
  
## <a name="return-types"></a>Tipos de retorno
**smallint**
  
|Valor de retorno|Cursor name|Variável de cursor|  
|---|---|---|
|1|O conjunto de resultados do cursor tem, ao menos, uma fila.<br /><br /> Para cursores insensitive e keyset, o conjunto de resultados terá ao menos uma linha.<br /><br /> Para cursores dinâmicos, o conjunto de resultados pode ter zero, uma ou mais linhas.|O cursor alocado a esta variável está aberto.<br /><br /> Para cursores insensitive e keyset, o conjunto de resultados terá ao menos uma linha.<br /><br /> Para cursores dinâmicos, o conjunto de resultados pode ter zero, uma ou mais linhas.|  
|0|O conjunto de resultados do cursor está vazio.*|O cursor alocado a esta variável está aberto, mas o conjunto de resultados está definitivamente vazio.*|  
|-1|O cursor está fechado.|O cursor alocado a esta variável está fechado.|  
|-2|Não aplicável.|Pode ser:<br /><br /> Nenhum cursor foi atribuído a esta variável OUTPUT pelo procedimento chamado anteriormente.<br /><br /> Um cursor foi atribuído a esta variável OUTPUT pelo procedimento chamado previamente, mas ele estava em estado de fechamento na conclusão do procedimento. Então, o cursor é desalocado e não é retornado ao procedimento de chamada.<br /><br /> Não há nenhum cursor atribuído à variável de cursor declarada.|  
|-3|Um cursor com o nome especificado não existe.|Uma variável de cursor com o nome especificado não existe, ou se existe, nenhum cursor foi alocado a ela ainda.|  
  
*Cursores dinâmicos nunca retornam esse resultado.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa a função `CURSOR_STATUS` para mostrar o status de um cursor antes e depois de ele ser aberto e fechado.
  
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
  
## <a name="see-also"></a>Consulte também
[Funções de cursor &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

