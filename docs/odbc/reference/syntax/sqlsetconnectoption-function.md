---
title: Função SQLSetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 518fa715656e16672c118e0e56588c7c15d16a15
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetconnectoption-function"></a>Função SQLSetConnectOption
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: Deprecated  
  
 **Resumo**  
 Em ODBC 3*. x*, a função ODBC 2.0 **SQLSetConnectOption** foi substituído pelo **SQLSetConnectAttr**. Para obter mais informações, veja [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 2*. x* aplicativo estiver trabalhando com um ODBC 3*. x* driver, consulte [mapeamento preterido funções](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>Remarks  
 Consulte [informações de ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), se o aplicativo será executado em um sistema operacional de 64 bits.  
  
> [!NOTE]  
>  Não há suporte para o atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzidas no ODBC 3.8 por **SQLSetConnectOption**. Aplicativos que usam a operação assíncrona no identificador de conexão devem usar **SQLSetConnectAttr**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
