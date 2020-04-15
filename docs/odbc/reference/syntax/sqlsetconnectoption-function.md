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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 263b15cb75fb5c0c7c1d7aa630a8da171b9765a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301591"
---
# <a name="sqlsetconnectoption-function"></a>Função SQLSetConnectOption
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: Preterido  
  
 **Resumo**  
 Em ODBC 3 *.x,* a função ODBC 2.0 **SQLSetConnectOption** foi substituída por **SQLSetConnectAttr**. Para obter mais informações, veja [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um aplicativo ODBC 2 *.x* estiver trabalhando com um driver ODBC 3 *.x,* consulte [Mapeamento de Funções Depreciadas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>Comentários  
 Consulte [As informações de 64 bits do ODBC,](../../../odbc/reference/odbc-64-bit-information.md)se o aplicativo for executado em um sistema operacional de 64 bits.  
  
> [!NOTE]  
>  O atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzido no ODBC 3.8 não é suportado pelo **SQLSetConnectOption**. Os aplicativos que usam a operação assíncrona no cabo de conexão devem usar **SQLSetConnectAttr**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
