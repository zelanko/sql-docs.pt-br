---
title: Função SQLPoolConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306897"
---
# <a name="sqlpoolconnect-function"></a>Função SQLPoolConnect
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,8: ODBC  
  
 **Resumo**  
 **SQLPoolConnect** será usado para criar uma nova conexão se nenhuma conexão no pool puder ser reutilizada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbc*  
 Entrada O identificador de conexão.  
  
 *hDbcInfoToken*  
 Entrada O identificador de token para a nova solicitação de conexão de aplicativo.  
  
 *wszOutConnectString*  
 Der Ponteiro para um buffer para a cadeia de conexão concluída. Após a conexão bem-sucedida com a fonte de dados de destino, esse buffer contém a cadeia de conexão concluída. Os aplicativos devem alocar pelo menos 1.024 caracteres para esse buffer.  
  
 Se *wszOutConnectString* for NULL, *cchConnectStringLen* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *wszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 Entrada Comprimento do buffer **wszOutConnectString* , em caracteres.  
  
 *cchConnectStringLen*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o caractere de terminação nula) disponível para retornar \*em *wszOutConnectString*. Se o número de caracteres disponíveis para retornar for maior ou igual a *cchConnectStringBuffer*, a cadeia de conexão concluída em \* *wszOutConnectString* será truncada para *cchConnectStringBuffer* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Semelhante a [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) para qualquer erro de validação de entrada, exceto que o Gerenciador de driver usará um **handletype** de SQL_HANDLE_DBC_INFO_TOKEN e um **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 O Gerenciador de driver garante que o identificador HENV pai de *hDbc* e *hDbcInfoToken* sejam os mesmos.  
  
 Ao contrário de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), não há nenhum argumento *DriverCompletion* para solicitar que os usuários insiram informações de conexão. Uma caixa de diálogo de solicitação não é permitida no cenário de Pooling.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexões com reconhecimento de driver deve implementar essa função.  
  
 Sempre que um driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o Gerenciador de driver retorna o erro para o aplicativo (em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) ou [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Sempre que um driver retornar SQL_SUCCESS_WITH_INFO, o Gerenciador de driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Quando um aplicativo usa [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), o *wszOutConnectString* será um buffer nulo (os últimos três parâmetros serão definidos como NULL, 0, NULL). Caso contrário, o driver deve retornar a cadeia de conexão de saída, que será retornada à chamada de [função SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) do aplicativo.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
