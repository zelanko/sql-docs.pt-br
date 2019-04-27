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
manager: craigg
ms.openlocfilehash: 62d22d1bf5fc3d01bf62afd2da6b3ebbc2bb0289
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742262"
---
# <a name="sqlsetconnectoption-function"></a>Função SQLSetConnectOption
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: Preterido  
  
 **Resumo**  
 Em ODBC 3 *. x*, a função ODBC 2.0 **SQLSetConnectOption** foi substituída por **SQLSetConnectAttr**. Para obter mais informações, veja [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 2 *. x* aplicativo está funcionando com um ODBC 3 *. x* driver, consulte [preterido funções de mapeamento de](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>Comentários  
 Ver [informações de ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md), se o aplicativo será executado em um sistema operacional de 64 bits.  
  
> [!NOTE]  
>  Não há suporte para o atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzidas no ODBC 3.8 por **SQLSetConnectOption**. Aplicativos que usam a operação assíncrona no identificador de conexão devem usar **SQLSetConnectAttr**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
