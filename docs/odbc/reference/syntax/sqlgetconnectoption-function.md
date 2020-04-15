---
title: Função SQLGetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94a29637365862990ea067f663023fae04a7af3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285566"
---
# <a name="sqlgetconnectoption-function"></a>Função SQLGetConnectOption
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: Preterido  
  
 **Resumo**  
 Em ODBC *3.x,* a função ODBC *2.x* **SQLGetConnectOption** foi substituída por **SQLGetConnectAttr**. Para obter mais informações, consulte [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um aplicativo ODBC *2.x* estiver trabalhando com um driver ODBC *3.x,* consulte [Mapeamento de Funções Depreciadas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no Apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
> 
> [!NOTE]
>  O atributo SQL_ASYNC_DBC_FUNCTION_ENABLE introduzido no ODBC 3.8 não é suportado pelo **SQLGetConnectOption**. Os aplicativos que usam a operação assíncrona em uma alça de conexão devem usar **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
