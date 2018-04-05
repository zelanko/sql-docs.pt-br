---
title: UPDATE - SQL comando | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fb2e4d3e3010eaba53b36de383c3365d82db289
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="update---sql-command"></a>SQL de atualização - comando
Atualiza os registros em uma tabela com novos valores.  
  
 O Driver de ODBC do Visual FoxPro oferece suporte a sintaxe de linguagem do Visual FoxPro nativo para este comando. Para obter informações específicas do driver, consulte **comentários de Driver**.  
  
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
  
 *DatabaseName1!* Especifica o nome de um banco de dados diferente do especificado com a fonte de dados que contém a tabela. Você deve incluir o nome do banco de dados que contém a tabela se o banco de dados não é atual. Inclua o delimitador de ponto de exclamação (!) depois do nome do banco de dados e antes do nome da tabela.  
  
 DEFINIR *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica as colunas que estão atualizadas e seus novos valores. Se você omitir a cláusula WHERE, cada linha na coluna é atualizada com o mesmo valor.  
  
 ONDE *FilterCondition1*[AND &#124; OU *FilterCondition2*...]  
 Especifica os registros que são atualizados com novos valores.  
  
 *FilterCondition* Especifica os critérios que os registros devem atender para ser atualizada com novos valores. Você pode incluir muitas condições de filtragem você deseja conectar-se com o operador e ou operador OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **vazio**() para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Remarks  
 UPDATE - SQL pode atualizar somente os registros em uma única tabela.  
  
 Ao contrário de substituição, a atualização - SQL usa o bloqueio de registro ao atualizar vários registros em tabelas aberto para acesso compartilhado. Isso reduz a contenção de registro em situações de multiusuários, mas pode reduzir o desempenho. Para obter desempenho máximo, abra a tabela para exclusivo use ou **FLOCK**() para bloquear a tabela.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Quando o aplicativo envia a instrução SQL ODBC atualização para a fonte de dados, o Driver de ODBC do Visual FoxPro converte o comando para o comando FoxProUPDATE Visual sem conversão.  
  
## <a name="see-also"></a>Consulte Também  
 [Exclua - o comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
