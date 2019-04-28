---
title: SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetDiagField function
ms.assetid: 395245ba-0372-43ec-b9a4-a29410d85a6d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fb158b2c11f48733c5eacb3827a43a3303c4a51
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657699"
---
# <a name="sqlgetdiagfield"></a>SQLGetDiagField
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client Especifica os seguintes campos de diagnósticos adicionais para `SQLGetDiagField`. Esses campos suportam relatórios bem-elaborados de erros para os aplicativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estão disponíveis em todos os registros de diagnóstico gerados em identificadores de conexão conectados ODBC e identificadores de instrução ODBC. Os campos são definidos em sqlncli.h.  
  
|Campo de registro de diagnóstico|Descrição|  
|------------------------------|-----------------|  
|SQL_DIAG_SS_LINE|Informa o número da linha de um procedimento armazenado que gera um erro. O valor de SQL_DIAG_SS_LINE só será útil se SQL_DIAG_SS_PROCNAME retornar um valor. O valor é retornado como um inteiro de 16 bits sem-sinal.|  
|SQL_DIAG_SS_MSGSTATE|O estado de uma mensagem de erro. Para obter informações sobre o estado da mensagem de erro, consulte [RAISERROR](/sql/t-sql/language-elements/raiserror-transact-sql). O valor é retornado como um inteiro de 32 bits com assinatura.|  
|SQL_DIAG_SS_PROCNAME|O nome do procedimento armazenado que gera um erro, se apropriado. O valor é retornado como uma cadeia de caracteres. O comprimento da cadeia de caracteres (em caracteres) depende da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele pode ser determinado chamando [SQLGetInfo](sqlgetinfo.md) solicitando o valor de SQL_MAX_PROCEDURE_NAME_LEN.|  
|SQL_DIAG_SS_SEVERITY|O nível de severidade da mensagem de erro associada. O valor é retornado como um inteiro de 32 bits com assinatura.|  
|SQL_DIAG_SS_SRVNAME|O nome do servidor no qual o erro ocorreu. O valor é retornado como uma cadeia de caracteres. O comprimento da cadeia de caracteres (em caracteres) é definido pela macro SQL_MAX_SQLSERVERNAME em sqlncli.h.|  
  
 Campos de diagnóstico específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contêm dados de caractere, SQL_DIAG_SS_PROCNAME e SQL_DIAG_SS_SRVNAME, retornam esses dados para o cliente como cadeia de caracteres com terminação nula, ANSI ou Unicode. Se necessário, a contagem de caracteres deve ser ajustada de acordo com a largura do caractere. Como opção, um tipo de dados C portátil, como TCHAR ou SQLTCHAR, pode ser usado para garantir o comprimento variável correto do programa.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client informa os códigos de função dinâmicos adicionais a seguir que identificam a última instrução do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentada. O código de função dinâmico é retornado no cabeçalho (record 0) do registro de diagnóstico definido e, portanto, está disponível em cada execução (bem-sucedida ou não).  
  
|Código de função dinâmico|Source|  
|---------------------------|------------|  
|SQL_DIAG_DFC_SS_ALTER_DATABASE|instrução ALTER DATABASE|  
|SQL_DIAG_DFC_SS_CHECKPOINT|Instrução CHECKPOINT|  
|SQL_DIAG_DFC_SS_CONDITION|O erro ocorreu nas cláusulas WHERE ou HAVING de uma instrução.|  
|SQL_DIAG_DFC_SS_CREATE_DATABASE|Instrução CREATE DATABASE|  
|SQL_DIAG_DFC_SS_CREATE_DEFAULT|Instrução CREATE DEFAULT|  
|SQL_DIAG_DFC_SS_CREATE_PROCEDURE|Instrução CREATE PROCEDURE|  
|SQL_DIAG_DFC_SS_CREATE_RULE|Instrução CREATE RULE|  
|SQL_DIAG_DFC_SS_CREATE_TRIGGER|instrução CREATE TRIGGER|  
|SQL_DIAG_DFC_SS_CURSOR_DECLARE|Instrução DECLARE CURSOR|  
|SQL_DIAG_DFC_SS_CURSOR_OPEN|Instrução OPEN|  
|SQL_DIAG_DFC_SS_CURSOR_FETCH|Instrução FETCH|  
|SQL_DIAG_DFC_SS_CURSOR_CLOSE|Instrução CLOSE|  
|SQL_DIAG_DFC_SS_DEALLOCATE_CURSOR|Instrução DEALLOCATE|  
|SQL_DIAG_DFC_SS_DBCC|Instrução DBCC|  
|SQL_DIAG_DFC_SS_DENY|instrução DENY|  
|SQL_DIAG_DFC_SS_DROP_DATABASE|instrução DROP DATABASE|  
|SQL_DIAG_DFC_SS_DROP_DEFAULT|Instrução DROP DEFAULT|  
|SQL_DIAG_DFC_SS_DROP_PROCEDURE|Instrução DROP PROCEDURE|  
|SQL_DIAG_DFC_SS_DROP_RULE|Instrução DROP RULE|  
|SQL_DIAG_DFC_SS_DROP_TRIGGER|instrução DROP TRIGGER|  
|SQL_DIAG_DFC_SS_DUMP_DATABASE|Instrução BACKUP ou DUMP DATABASE|  
|SQL_DIAG_DFC_SS_DUMP_TABLE|Instrução DUMP TABLE|  
|SQL_DIAG_DFC_SS_DUMP_TRANSACTION|Instrução BACKUP ou DUMP TRANSACTION. Também é retornado para uma instrução de ponto de verificação se o **trunc. log no ponto de verificação.** opção de banco de dados está ativada.|  
|SQL_DIAG_DFC_SS_GOTO|Instrução de controle de fluxo GOTO|  
|SQL_DIAG_DFC_SS_INSERT_BULK|Instrução INSERT BULK|  
|SQL_DIAG_DFC_SS_KILL|Instrução KILL|  
|SQL_DIAG_DFC_SS_LOAD_DATABASE|Instrução LOAD ou RESTORE DATABASE|  
|SQL_DIAG_DFC_SS_LOAD_HEADERONLY|Instrução LOAD ou RESTORE HEADERONLY|  
|SQL_DIAG_DFC_SS_LOAD_TABLE|Instrução LOAD TABLE|  
|SQL_DIAG_DFC_SS_LOAD_TRANSACTION|Instrução LOAD ou RESTORE TRANSACTION|  
|SQL_DIAG_DFC_SS_PRINT|instrução PRINT|  
|SQL_DIAG_DFC_SS_RAISERROR|instrução RAISERROR|  
|SQL_DIAG_DFC_SS_READTEXT|Instrução READTEXT|  
|SQL_DIAG_DFC_SS_RECONFIGURE|Instrução RECONFIGURE|  
|SQL_DIAG_DFC_SS_RETURN|Instrução de controle de fluxo RETURN|  
|SQL_DIAG_DFC_SS_SELECT_INTO|instrução SELECT INTO|  
|SQL_DIAG_DFC_SS_SET|Instrução SET (genérica, todas as opções)|  
|SQL_DIAG_DFC_SS_SET_IDENTITY_INSERT|Instrução SET IDENTITY_INSERT|  
|SQL_DIAG_DFC_SS_SET_ROW_COUNT|Instrução SET ROWCOUNT|  
|SQL_DIAG_DFC_SS_SET_STATISTICS|Instruções SET STATISTICS IO ou SET STATISTICS TIME|  
|SQL_DIAG_DFC_SS_SET_TEXTSIZE|Instrução SET TEXTSIZE|  
|SQL_DIAG_DFC_SS_SETUSER|Instrução SETUSER|  
|SQL_DIAG_DFC_SS_SET_XCTLVL|Instrução SET TRANSACTION ISOLATION LEVEL|  
|SQL_DIAG_DFC_SS_SHUTDOWN|Instrução SHUTDOWN|  
|SQL_DIAG_DFC_SS_TRANS_BEGIN|Instrução BEGIN TRAN|  
|SQL_DIAG_DFC_SS_TRANS_COMMIT|Instrução COMMIT TRAN|  
|SQL_DIAG_DFC_SS_TRANS_PREPARE|Preparar para confirmar uma transação distribuída|  
|SQL_DIAG_DFC_SS_TRANS_ROLLBACK|Instrução ROLLBACK TRAN|  
|SQL_DIAG_DFC_SS_TRANS_SAVE|Instrução SAVE TRAN|  
|SQL_DIAG_DFC_SS_TRUNCATE_TABLE|Instrução TRUNCATE TABLE|  
|SQL_DIAG_DFC_SS_UPDATE_STATISTICS|Instrução UPDATE STATISTICS|  
|SQL_DIAG_DFC_SS_UPDATETEXT|instrução UPDATETEXT|  
|SQL_DIAG_DFC_SS_USE|instrução USE|  
|SQL_DIAG_DFC_SS_WAITFOR|Instrução de controle de fluxo WAITFOR|  
|SQL_DIAG_DFC_SS_WRITETEXT|Instrução WRITETEXT|  
  
## <a name="sqlgetdiagfield-and-table-valued-parameters"></a>SQLGetDiagField e parâmetros com valor de tabela  
 SQLGetDiagField pode ser usado para recuperar dois campos de diagnóstico: SQL_DIAG_SS_TABLE_COLUMN_NUMBER e SQL_DIAG_SS_TABLE_ROW_NUMBER. Esses campos ajudam a determinar qual valor gerou o erro ou a mensagem de advertência associada ao registro de diagnóstico.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLGetDiagField](https://go.microsoft.com/fwlink/?LinkId=59352)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
