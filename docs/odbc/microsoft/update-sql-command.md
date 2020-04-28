---
title: Atualizar-comando SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818811c18ed52cef5bdb1c4d97f947bb86e67422
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307637"
---
# <a name="update---sql-command"></a>UPDATE – comando SQL
Atualiza os registros em uma tabela com novos valores.  
  
 O driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro para este comando. Para obter informações específicas do driver, consulte **comentários do driver**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumentos  
 ATUALIZAÇÃO [ *DatabaseName1!*] *TableName1*  
 Especifica a tabela na qual os registros são atualizados com novos valores.  
  
 *DatabaseName1!* Especifica o nome de um banco de dados que não seja o especificado com a fonte que contém a tabela. Você deve incluir o nome do banco de dados que contém a tabela se o banco de dados não for o atual. Inclua o delimitador de ponto de exclamação (!) após o nome do banco de dados e antes do nome da tabela.  
  
 Definir *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica as colunas que são atualizadas e seus novos valores. Se você omitir a cláusula WHERE, todas as linhas da coluna serão atualizadas com o mesmo valor.  
  
 EM que *FilterCondition1*[e &#124; ou *FilterCondition2*...]  
 Especifica os registros que são atualizados com novos valores.  
  
 *FilterCondition* especifica os critérios que os registros devem atender para serem atualizados com novos valores. Você pode incluir quantas condições de filtro desejar, conectando-as com o operador AND ou OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica ou pode usar **Empty**() para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Comentários  
 UPDATE-SQL pode atualizar somente os registros em uma única tabela.  
  
 Ao contrário de REPLACE, UPDATE-SQL usa o bloqueio de registro ao atualizar vários registros em tabelas abertas para acesso compartilhado. Isso reduz a contenção de registros em situações multiusuários, mas pode reduzir o desempenho. Para obter o máximo de desempenho, abra a tabela para uso exclusivo ou use **Flock**() para bloquear a tabela.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Quando o aplicativo envia a atualização da instrução SQL do ODBC para a fonte de dados, o driver ODBC do Visual FoxPro converte o comando no comando FoxProUPDATE do Visual sem tradução.  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE-comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
