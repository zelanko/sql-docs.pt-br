---
title: ATUALIZAÇÃO - Comando SQL | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307637"
---
# <a name="update---sql-command"></a>UPDATE – comando SQL
Atualiza registros em uma tabela com novos valores.  
  
 O Visual FoxPro ODBC Driver suporta a sintaxe nativa visual foxpro para este comando. Para obter informações específicas do motorista, consulte **Observações do motorista**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argumentos  
 ATUALIZAÇÃO [ *DatabaseName1!*] *Nome da tabela1*  
 Especifica a tabela em que os registros são atualizados com novos valores.  
  
 *Banco de dadosName1!* especifica o nome de um banco de dados diferente do banco de dados especificado com a fonte de dados que contém a tabela. Você deve incluir o nome do banco de dados que contém a tabela se o banco de dados não for o atual. Inclua o ponto de exclamação (!) delimitador após o nome do banco de dados e antes do nome da tabela.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Especifica as colunas atualizadas e seus novos valores. Se você omite a cláusula WHERE, todas as linhas da coluna serão atualizadas com o mesmo valor.  
  
 ONDE *FilterCondition1*[E &#124; OU *FiltroCondição2*...]  
 Especifica os registros atualizados com novos valores.  
  
 *FilterCondition* especifica os critérios que os registros devem atender para serem atualizados com novos valores. Você pode incluir quantas condições de filtro quiser, conectando-as com o operador And ou OR. Você também pode usar o operador NOT para reverter o valor de uma expressão lógica, ou você pode usar **EMPTY**( ) para verificar se há um campo vazio.  
  
## <a name="remarks"></a>Comentários  
 ATUALIZAÇÃO - O SQL pode atualizar apenas registros em uma única tabela.  
  
 Ao contrário do REPLACE, UPDATE - SQL usa bloqueio de registros ao atualizar vários registros em tabelas abertas para acesso compartilhado. Isso reduz a contenção de registros em situações de vários usuários, mas pode reduzir o desempenho. Para o máximo desempenho, abra a mesa para uso exclusivo ou use **FLOCK**( ) para bloquear a mesa.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Quando seu aplicativo envia a declaração ODBC SQL UPDATE para a fonte de dados, o Driver Visual FoxPro ODBC converte o comando no comando Visual FoxProUPDATE sem tradução.  
  
## <a name="see-also"></a>Consulte Também  
 [DELETE - Comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
