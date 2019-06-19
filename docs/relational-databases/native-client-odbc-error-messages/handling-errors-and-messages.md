---
title: Tratamento de erros e mensagens | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ca55861daaeb32eaf5cce4fc70e09f54622a3f13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740487"
---
# <a name="handling-errors-and-messages"></a>Tratando de erros e mensagens
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Quando um aplicativo chama uma função ODBC, o driver executa a função e retorna informações de diagnóstico de duas maneiras: Um código de retorno indica o êxito ou falha de uma função ODBC geral e os registros de diagnóstico fornecem informações detalhadas sobre a função. Os registros de diagnóstico incluem um registro de cabeçalho e registros de status. Pelo menos um registro de diagnóstico, o registro de cabeçalho, será retornado, mesmo que a função tenha êxito.  
  
 As informações de diagnóstico são usadas em tempo de desenvolvimento para capturar erros de programação, como identificadores inválidos e erros de sintaxe em instruções SQL embutidas em código. Elas também são usadas em tempo de execução para capturar erros e avisos de tempo de execução, como truncamento de dados, violações de regras e erros de sintaxe em instruções SQL inseridas pelo usuário. Em geral, a lógica de programação se baseia em códigos de retorno.  
  
 Por exemplo, depois que um aplicativo chama **SQLFetch** para recuperar as linhas em um conjunto de resultados, o código de retorno indica se o final do conjunto de resultados foi atingido (SQL_NO_DATA), se nenhuma mensagem informativa foram retornadas (SQL_SUCCESS_ WITH_INFO), ou se um erro (SQL_ERROR).  
  
 Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retorna algo diferente de SQL_SUCCESS, o aplicativo pode chamar **SQLGetDiagRec** para recuperar qualquer informação ou mensagens de erro. Use **SQLGetDiagRec** para rolar para cima e para a mensagem definido se não houver mais de uma mensagem.  
  
 O código de retorno SQL_INVALID_HANDLE sempre indica um erro de programação e nunca deve ser encontrado em tempo de execução. Todos os outros códigos de retorno fornecem informações, embora SQL_ERROR possa indicar um erro de programação.  
  
 O original [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API nativa, DB-Library para C, permite que um aplicativo para instalar o tratamento de erro de retorno de chamada e funções de manipulação de mensagens que retornam erros ou mensagens. Algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como PRINT, RAISERROR, DBCC e SET, retornam seus resultados para a função de manipulador de mensagens de DB-Library e não para um conjunto de resultados. Porém, a API ODBC não tem nenhum recurso de retorno de chamada. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client detecta mensagens voltando do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele define o código de retorno ODBC como SQL_SUCCESS_WITH_INFO ou SQL_ERROR e retorna a mensagem como um ou mais registros de diagnóstico. Portanto, um aplicativo ODBC deve testar cuidadosamente esses códigos e chamada de retorno **SQLGetDiagRec** para recuperar dados da mensagem.  
  
 Para obter informações sobre como rastrear erros, confira [Rastreamento do acesso a dados](https://go.microsoft.com/fwlink/?LinkId=125805). Para obter informações sobre os aprimoramentos para rastreamento de erro adicionado ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [acessando informações de diagnóstico no Log de eventos estendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Processando instruções que geram mensagens](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [Registros e campos de diagnóstico](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [Números de erro nativos](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40;códigos de erro ODBC&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [Mensagens de erro](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
