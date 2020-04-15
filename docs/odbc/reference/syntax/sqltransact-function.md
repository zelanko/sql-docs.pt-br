---
title: Função SQLTransact | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a4f1da36a7c233e9a1b5832ee83e86a5c1f77d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287076"
---
# <a name="sqltransact-function"></a>Função SQLTransact
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: Preterido  
  
 **Resumo**  
 Em ODBC *3.x,* a função ODBC *2.x* **SQLTransact** foi substituída por **SQLEndTran**. Para obter mais informações, consulte [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  O atributo SQL_ASYNC_DBC_FUNCTION_ENABLE, que foi introduzido no ODBC 3.8, não é suportado pelo **SQLTransact**. Os aplicativos que utilizam uma operação assíncrona em uma alça de conexão devem usar **O SQLEndTran**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
