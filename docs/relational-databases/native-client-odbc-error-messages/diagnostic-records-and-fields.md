---
title: "Registros de diagnóstico e campos | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b2c800550b992735c0af6854a83d5ea28a2c597
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="diagnostic-records-and-fields"></a>Registros e campos de diagnóstico
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Os registros de diagnóstico são associados com ambiente, conexão, instrução ou identificadores de descritor ODBC. Quando uma função ODBC gera um código de retorno diferente de SQL_SUCCESS ou SQL_INVALID_HANDLE, o identificador chamado pela função possui registros de diagnóstico associados que contêm mensagens de erro ou mensagens informativas. Esses registros são retidos até que outra função seja chamada com aquele identificador. Depois disso, são descartados. Não há limite para o número de registros de diagnóstico que podem ser associados a um identificador de uma só vez.  
  
 Há dois tipos de registros de diagnóstico: cabeçalho e status. O registro de cabeçalho é registro 0; quando há registros de status, eles são registros 1 e posteriores. Os registros de diagnóstico contêm campos diferentes para o registro de cabeçalho e os registros de status. Os componentes ODBC também podem definir seus próprios campos de registro de diagnóstico.  
  
 Os campos no registro de cabeçalho contêm informações gerais sobre a execução de uma função, incluindo o código de retorno, a contagem de linhas, o número de registros de status e o tipo de instruções executadas. O registro de cabeçalho sempre é criado, a menos que uma função ODBC retorne SQL_INVALID_HANDLE. Para obter uma lista completa dos campos no registro de cabeçalho, consulte [SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md).  
  
 Os campos dos registros de status contêm informações sobre erros ou avisos específicos retornados pelo Gerenciador de Driver ODBC, driver ou fonte de dados, incluindo o SQLSTATE, número do erro nativo, mensagem de diagnóstico, número da coluna e número da linha. Os registros de status só são criados se a função retornar SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA ou SQL_STILL_EXECUTING. Para obter uma lista completa dos campos dos registros de status, consulte **SQLGetDiagField**.  
  
 **SQLGetDiagRec** recupera um único registro de diagnóstico junto com seu ODBC SQLSTATE, número de erro nativo e campos de mensagem de diagnóstico. Essa funcionalidade é semelhante do ODBC 2. *x * SQLError** função. A função mais simples de tratamento de erros em ODBC 3. *x* é chamar repetidamente **SQLGetDiagRec** começando com o *RecNumber* parâmetro definido como 1 e aumentando *RecNumber* por 1 até **SQLGetDiagRec** retorna SQL_NO_DATA. Isso é equivalente a um ODBC 2. *x* aplicativo que chama **SQLError** até ele retornar SQL_NO_DATA_FOUND.  
  
 ODBC 3. *x* dá suporte a muito mais informações de diagnósticas que o ODBC 2. *x*. Essas informações são armazenadas nos campos adicionais recuperados por meio de registros de diagnóstico **SQLGetDiagField**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client tem campos de diagnósticos específicos de driver que podem ser recuperados com **SQLGetDiagField**. Os rótulos para esses campos específicos de driver são definidos em sqlncli.h. Use esses rótulos para recuperar o estado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nível de severidade, nome do servidor, nome do procedimento e número de linha associado a cada registro de diagnóstico. Além disso, SQLNCLI. h conterá definições dos códigos do driver usa para identificar instruções Transact-SQL se um aplicativo chamar **SQLGetDiagField** com *DiagIdentifier* definido como SQL_DIAG_DYNAMIC_ FUNCTION_CODE.  
  
 **SQLGetDiagField** é processada pelo Gerenciador de Driver ODBC usando as informações de erro, ele armazena em cache do driver subjacente. O Gerenciador de Driver ODBC não armazena em cache os campos de diagnóstico específicos de driver até que seja estabelecida uma conexão bem-sucedida. **SQLGetDiagField** retornará SQL_ERROR se for chamado para obter os campos de diagnóstico específicos de driver antes de uma conexão bem-sucedida foi concluída. Se uma função de conexão ODBC retornar SQL_SUCCESS_WITH_INFO, os campos de diagnóstico específicos de driver para a função de conexão ainda não estarão disponíveis. Você pode iniciar uma chamada **SQLGetDiagField** para campos de diagnóstico específicos de driver apenas após você ter feito ODBC outra chamada de função após a função de conexão.  
  
 A maioria dos erros relatados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client pode ser diagnosticado usando apenas as informações retornadas por **SQLGetDiagRec**. Em alguns casos, porém, as informações retornadas pelos campos de diagnóstico específicos de driver são importantes no diagnóstico de um erro. Ao codificar um identificador de erro ODBC para aplicativos que usam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC Native Client, é recomendável também usar **SQLGetDiagField** para recuperar pelo menos o SQL_DIAG_SS_MSGSTATE e SQL_DIAG_SS_SEVERITY campos específicos do driver. Se um erro em particular for gerado em vários locais no código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_DIAG_SS_MSGSTATE indicará a um engenheiro de suporte da Microsoft onde especificamente o erro foi gerado, o que muitas vezes ajuda no diagnóstico de um problema.  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
