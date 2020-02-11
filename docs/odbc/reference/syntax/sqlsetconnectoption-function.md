---
title: Função SQLSetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectOption
helpviewer_keywords:
- SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b429e499cccaad553236b4ebee78374c69c7c4dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093007"
---
# <a name="sqlsetconnectoption-function"></a>Função SQLSetConnectOption
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: preterida  
  
 **Resumo**  
 No ODBC 3 *. x*, a função **SQLSetConnectOption** do ODBC 2,0 foi substituída por **SQLSetConnectAttr**. Para obter mais informações, veja [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
> [!NOTE]
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC 2 *. x* está trabalhando com um driver ODBC 3 *. x* , consulte [mapeando funções preteridas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>Comentários  
 Consulte [informações de ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md), se seu aplicativo for executado em um sistema operacional de 64 bits.  
  
> [!NOTE]  
>  O atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzido no ODBC 3,8 não é suportado pelo **SQLSetConnectOption**. Os aplicativos que usam a operação assíncrona no identificador de conexão devem usar **SQLSetConnectAttr**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
