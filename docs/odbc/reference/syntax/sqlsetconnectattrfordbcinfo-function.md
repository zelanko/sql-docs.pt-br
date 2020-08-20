---
description: Função SQLSetConnectAttrForDbcInfo
title: Função SQLSetConnectAttrForDbcInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7380ba8682deb7424c363b28d42ecf3980755daf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499556"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Função SQLSetConnectAttrForDbcInfo
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,81: ODBC  
  
 **Resumo**  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr**, mas define o atributo no token de informações de conexão em vez de no identificador de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hDbcInfoToken*  
 Entrada Identificador de token.  
  
 *Atributo*  
 Entrada Atributo a ser definido. A lista de atributos válidos é específica do driver e a mesma para [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 Entrada Ponteiro para o valor a ser associado ao *atributo*. Dependendo do valor do *atributo*, *ValuePtr* será um valor inteiro sem sinal de 32 bits ou apontará para uma cadeia de caracteres de caractere terminada em nulo. Observe que, se o argumento de *atributo* for um valor específico de driver, o valor em *ValuePtr* poderá ser um inteiro assinado.  
  
 *StringLength*  
 Entrada Se o *atributo* for um atributo definido pelo ODBC e *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se o *atributo* for um atributo definido pelo ODBC e *ValuePtr* for um inteiro, *StringLength* será ignorado.  
  
 Se o *atributo* for um atributo definido por Driver, o aplicativo indicará a natureza do atributo para o Gerenciador de driver, definindo o argumento *StringLength* . *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* for um ponteiro para uma cadeia de caracteres, *StringLength* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *StringLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, o *StringLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), exceto pelo fato de que o Gerenciador de driver usará um **handletype** de SQL_HANDLE_DBC_INFO_TOKEN e um **identificador** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr**, mas define o atributo no token de informações de conexão, em vez de no identificador de conexão. Por exemplo, se **SQLSetConnectAttr** não reconhecer um atributo, **SQLSetConnectAttrForDbcInfo** também deverá retornar SQL_ERROR para esse atributo.  
  
 Sempre que o driver retorna SQL_ERROR ou SQL_INVALID_HANDLE, o driver deve ignorar esse atributo para computar a ID do pool. Além disso, o Gerenciador de driver obterá as informações de diagnóstico de *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Portanto, um aplicativo pode recuperar detalhes sobre por que alguns atributos não podem ser definidos.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexões com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
