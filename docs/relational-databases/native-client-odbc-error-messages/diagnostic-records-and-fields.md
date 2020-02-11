---
title: Registros e campos de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5bffbd7ce22bf3e1e906e68e880fb76bee36c4b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783660"
---
# <a name="diagnostic-records-and-fields"></a>Registros e campos de diagnóstico
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os registros de diagnóstico são associados com ambiente, conexão, instrução ou identificadores de descritor ODBC. Quando uma função ODBC gera um código de retorno diferente de SQL_SUCCESS ou SQL_INVALID_HANDLE, o identificador chamado pela função possui registros de diagnóstico associados que contêm mensagens de erro ou mensagens informativas. Esses registros são retidos até que outra função seja chamada com aquele identificador. Depois disso, são descartados. Não há limite para o número de registros de diagnóstico que podem ser associados a um identificador de uma só vez.  
  
 Há dois tipos de registros de diagnóstico: cabeçalho e status. O registro de cabeçalho é registro 0; quando há registros de status, eles são registros 1 e posteriores. Os registros de diagnóstico contêm campos diferentes para o registro de cabeçalho e os registros de status. Os componentes ODBC também podem definir seus próprios campos de registro de diagnóstico.  
  
 Os campos no registro de cabeçalho contêm informações gerais sobre a execução de uma função, incluindo o código de retorno, a contagem de linhas, o número de registros de status e o tipo de instruções executadas. O registro de cabeçalho sempre é criado, a menos que uma função ODBC retorne SQL_INVALID_HANDLE. Para obter uma lista completa de campos no registro de cabeçalho, consulte [SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md).  
  
 Os campos dos registros de status contêm informações sobre erros ou avisos específicos retornados pelo Gerenciador de Driver ODBC, driver ou fonte de dados, incluindo o SQLSTATE, número do erro nativo, mensagem de diagnóstico, número da coluna e número da linha. Os registros de status só são criados se a função retornar SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA ou SQL_STILL_EXECUTING. Para obter uma lista completa de campos nos registros de status, consulte **SQLGetDiagField**.  
  
 **SQLGetDiagRec** recupera um único registro de diagnóstico junto com seus campos do ODBC SQLSTATE, número de erro nativo e diagnóstico-Message. Essa funcionalidade é semelhante ao ODBC 2. função _x_**SqlError** . A função de tratamento de erros mais simples no ODBC 3. *x* é chamar repetidamente **SQLGetDiagRec** começando com o parâmetro *RecNumber* definido como 1 e incrementando *RecNumber* em 1 até que **SQLGetDiagRec** retorne SQL_NO_DATA. Isso é equivalente a um ODBC 2. aplicativo *x* chamando **SqlError** até que ele retorne SQL_NO_DATA_FOUND.  
  
 ODBC 3. *x* dá suporte a muito mais informações de diagnóstico do que o ODBC 2. *x*. Essas informações são armazenadas em campos adicionais nos registros de diagnóstico recuperados usando **SQLGetDiagField**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client tem campos de diagnóstico específicos do driver que podem ser recuperados com **SQLGetDiagField**. Os rótulos para esses campos específicos de driver são definidos em sqlncli.h. Use esses rótulos para recuperar o estado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nível de severidade, nome do servidor, nome do procedimento e número de linha associado a cada registro de diagnóstico. Além disso, sqlncli. h contém definições dos códigos que o driver usa para identificar instruções Transact-SQL se um aplicativo chama **SQLGetDiagField** com *DiagIdentifier* definido como SQL_DIAG_DYNAMIC_FUNCTION_CODE.  
  
 O **SQLGetDiagField** é processado pelo Gerenciador de driver ODBC usando informações de erro que ele armazena em cache do driver subjacente. O Gerenciador de Driver ODBC não armazena em cache os campos de diagnóstico específicos de driver até que seja estabelecida uma conexão bem-sucedida. **SQLGetDiagField** retornará SQL_ERROR se for chamado para obter campos de diagnóstico específicos do driver antes da conclusão de uma conexão bem-sucedida. Se uma função de conexão ODBC retornar SQL_SUCCESS_WITH_INFO, os campos de diagnóstico específicos de driver para a função de conexão ainda não estarão disponíveis. Você pode iniciar a chamada de **SQLGetDiagField** para campos de diagnóstico específicos do driver somente depois de ter feito outra chamada de função ODBC após a função de conexão.  
  
 A maioria dos erros relatados pelo driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pode ser efetivamente diagnosticada usando apenas as informações retornadas pelo **SQLGetDiagRec**. Em alguns casos, porém, as informações retornadas pelos campos de diagnóstico específicos de driver são importantes no diagnóstico de um erro. Ao codificar um manipulador de erro ODBC para aplicativos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam o driver ODBC do Native Client, também é uma boa ideia usar o **SQLGetDiagField** para recuperar pelo menos os SQL_DIAG_SS_MSGSTATE e SQL_DIAG_SS_SEVERITY campos específicos do driver. Se um erro em particular for gerado em vários locais no código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_DIAG_SS_MSGSTATE indicará a um engenheiro de suporte da Microsoft onde especificamente o erro foi gerado, o que muitas vezes ajuda no diagnóstico de um problema.  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
