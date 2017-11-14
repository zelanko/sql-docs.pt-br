---
title: "Função SQLSetConnectAttrForDbcInfo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ffe1bf224a28d7ff1151033576abcd5f10f56ed
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Função SQLSetConnectAttrForDbcInfo
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr**, mas ela define o atributo no token de informações de conexão em vez de no identificador da conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 [Entrada] Identificador de token.  
  
 *Atributo*  
 [Entrada] Atributo a ser definido. A lista de atributos válidos é específico do driver e os mesmos para [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado aos *atributo*. Dependendo do valor de *atributo*, *ValuePtr* será um valor inteiro não assinado de 32 bits ou aponta para uma cadeia de caracteres terminada em nulo. Observe que, se o *atributo* argumento é um driver específico, o valor em *ValuePtr* pode ser um inteiro com sinal.  
  
 *StringLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* é um inteiro, *StringLength* será ignorado.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *StringLength* argumento. *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *StringLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, em seguida, *StringLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contém um valor de comprimento fixo, em seguida, *StringLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e um **tratar** de *hDbcInfoToken* .  
  
## <a name="remarks"></a>Comentários  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr**, mas ela define o atributo no token de informações de conexão, em vez de no identificador da conexão. Por exemplo, se **SQLSetConnectAttr** não reconhece um atributo **SQLSetConnectAttrForDbcInfo** também deve retornar SQL_ERROR para esse atributo.  
  
 Sempre que o driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o driver deve ignorar esse atributo para calcular a ID do pool. Além disso, o Gerenciador de Driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO para o aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Portanto, um aplicativo pode recuperar detalhes sobre por que alguns atributos não podem ser definidos.  
  
 Aplicativos não devem chamar esta função diretamente. Um driver ODBC que oferece suporte ao pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

