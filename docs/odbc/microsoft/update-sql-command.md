---
title: UPDATE – comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbd5ec98791d782fe7ad1fdb1e1884b646dcf9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632553"
---
# <a name="update---sql-command"></a>UPDATE – comando SQL
Atualiza os registros em uma tabela com novos valores.  
  
 O Driver de ODBC do Visual FoxPro dá suporte à sintaxe de linguagem do Visual FoxPro nativo para esse comando. Para obter informações específicas do driver, consulte **Driver comentários**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumentos  
 UPDATE [ *DatabaseName1!* ] *TableName1*  
 Especifica a tabela na qual os registros são atualizados com novos valores.  
  
 *DatabaseName1!* Especifica o nome de um banco de dados que não seja o banco de dados especificado com a fonte de dados que contém a tabela. Você deve incluir o nome do banco de dados que contém a tabela se o banco de dados não for atual. Inclua o delimitador de ponto de exclamação (!) após o nome do banco de dados e antes do nome da tabela.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica as colunas que são atualizadas e seus novos valores. Se você omitir a cláusula WHERE, cada linha na coluna é atualizada com o mesmo valor.  
  
 Em que *FilterCondition1*[AND &#124; ou *FilterCondition2*...]  
 Especifica os registros que são atualizados com novos valores.  
  
 *FilterCondition* Especifica os critérios que os registros devem atender para serem atualizados com novos valores. Você pode incluir quantos condições de filtragem desejar, conectar-se com o operador e ou operador OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **vazio**() para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Comentários  
 ATUALIZAÇÃO - SQL pode atualizar somente os registros em uma única tabela.  
  
 Ao contrário de REPLACE, a atualização - SQL usa bloqueio de registro quando Atualizando vários registros nas tabelas aberto para acesso compartilhado. Isso reduz a contenção de registros em situações de multiusuários, mas pode reduzir o desempenho. Para obter máximo desempenho, abra a tabela para exclusiva de uso ou usar **USAM**() para bloquear a tabela.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando seu aplicativo envia a instrução SQL ODBC atualização para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando FoxProUPDATE Visual sem tradução.  
  
## <a name="see-also"></a>Consulte também  
 [DELETE – comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
