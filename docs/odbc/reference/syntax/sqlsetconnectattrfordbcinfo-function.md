---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15366693f212690176620bd1b395dae856ff1302
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537294"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Função SQLSetConnectAttrForDbcInfo
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr**, mas ele define o atributo no token de informações de conexão em vez de no identificador de conexão.  
  
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
 [Entrada] Identificador de token.  
  
 *Atributo*  
 [Entrada] Atributo a ser definido. A lista de atributos válidos é específico do driver e os mesmos para [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado aos *atributo*. Dependendo do valor de *atributo*, *ValuePtr* será um valor inteiro sem sinal de 32 bits ou apontará para uma cadeia de caracteres terminada em nulo. Observe que, se o *atributo* argumento é um valor específico do driver, o valor na *ValuePtr* pode ser um inteiro com sinal.  
  
 *StringLength*  
 [Entrada] Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *atributo* é um atributo definido pelo ODBC e *ValuePtr* é um inteiro *StringLength* será ignorado.  
  
 Se *atributo* é um atributo definido pelo driver, o aplicativo indica a natureza do atributo para o Gerenciador de Driver, definindo o *StringLength* argumento. *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *StringLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, em seguida, *StringLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, então *StringLength* é SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), exceto que o Gerenciador de Driver usará uma **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **manipular** de *hDbcInfoToken* .  
  
## <a name="remarks"></a>Comentários  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr**, mas ele define o atributo no token de informações de conexão, em vez de no identificador de conexão. Por exemplo, se **SQLSetConnectAttr** não reconhece um atributo **SQLSetConnectAttrForDbcInfo** também deve retornar SQL_ERROR para esse atributo.  
  
 Sempre que o driver retornará SQL_ERROR ou SQL_INVALID_HANDLE, o driver deve ignorar esse atributo para calcular a ID do pool. Além disso, o Gerenciador de Driver obterá as informações de diagnóstico da *hDbcInfoToken*e retornar SQL_SUCCESS_WITH_INFO para o aplicativo nos [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Portanto, um aplicativo pode recuperar detalhes sobre por que alguns atributos não podem ser definidos.  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
