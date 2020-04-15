---
title: SQLSetConnectAttrForDbcInfo Function | Microsoft Docs
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
ms.openlocfilehash: 9f43a0fc6cd02fe566579a543667f9a4c4c1a108
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301883"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>Função SQLSetConnectAttrForDbcInfo
**Conformidade**  
 Versão introduzida: ODBC 3.81 Normas De conformidade: ODBC  
  
 **Resumo**  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr,** mas define o atributo no token de informações de conexão em vez de no cabo de conexão.  
  
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
 [Entrada] Alça de token.  
  
 *Atributo*  
 [Entrada] Atributo ao conjunto. A lista de atributos válidos é específica do driver e a mesma de [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 *ValuePtr*  
 [Entrada] Ponteiro para o valor a ser associado com *Atributo*. Dependendo do valor de *Atributo,* *ValuePtr* será um valor inteiro não assinado de 32 bits ou apontará para uma seqüência de caracteres com término nulo. Observe que se o argumento *Atributo* for um valor específico do driver, o valor no *ValuePtr* pode ser um inteiro assinado.  
  
 *Stringlength*  
 [Entrada] Se *Atributo* for um atributo definido pelo ODBC e *o ValuePtr* aponta para uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento de **ValuePtr*. Para dados de seqüência de caracteres, este argumento deve conter o número de bytes na seqüência de caracteres.  
  
 Se *Atributo* for um atributo definido pelo ODBC e *o ValuePtr* for um inteiro, *StringLength* será ignorado.  
  
 Se *Atributo* for um atributo definido pelo driver, o aplicativo indicará a natureza do atributo ao Gerenciador de driver, definindo o argumento *StringLength.* *StringLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma seqüência de caracteres, então *StringLength* é o comprimento da seqüência ou SQL_NTS.  
  
-   Se *ValuePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *StringLength*. Isso coloca um valor negativo em *StringLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma seqüência de caracteres ou uma seqüência binária, então *StringLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, então *StringLength* será SQL_IS_INTEGER ou SQL_IS_UINTEGER, conforme apropriado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O mesmo que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), exceto que o Driver Manager usará um **HandleType** de SQL_HANDLE_DBC_INFO_TOKEN e uma **alça** de *hDbcInfoToken*.  
  
## <a name="remarks"></a>Comentários  
 **SQLSetConnectAttrForDbcInfo** é o mesmo que **SQLSetConnectAttr,** mas define o atributo no token de informações de conexão, em vez de no cabo de conexão. Por exemplo, se **o SQLSetConnectAttr** não reconhecer um atributo, **o SQLSetConnectAttrForDbcInfo** também deve retornar SQL_ERROR para esse atributo.  
  
 Sempre que o motorista retorna SQL_ERROR ou SQL_INVALID_HANDLE, o motorista deve ignorar esse atributo para calcular o ID do pool. Além disso, o Driver Manager obterá as informações de diagnóstico do *hDbcInfoToken*e retornará SQL_SUCCESS_WITH_INFO ao aplicativo no [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) e [no SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md). Portanto, um aplicativo pode recuperar detalhes sobre por que alguns atributos não podem ser definidos.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
