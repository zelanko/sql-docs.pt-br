---
title: Função SQLSetScrollOptions | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287257"
---
# <a name="sqlsetscrolloptions-function"></a>Função SQLSetScrollOptions
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: Preterido  
  
 **Resumo**  
 Em ODBC *3.x,* a função ODBC 2.0 **SQLSetScrollOptions** foi substituída por chamadas para **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um aplicativo ODBC *2.x* estiver trabalhando com um driver ODBC *3.x,* consulte [Mapeamento de Funções Depreciadas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no Apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
> 
> [!NOTE]
>  Quando o Gerenciador de driver mapeia **SQLSetScrollOptions** para um aplicativo que trabalha com um driver ODBC *3.x* que não suporta **SQLSetScrollOptions,** o Gerenciador de driver define a opção de declaração SQL_ROWSET_SIZE, não o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE, para o argumento *RowsetSize* no **SQLSetScrollOption**. Como resultado, **sqlsetscrolloptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele só pode ser usado quando busca várias linhas por uma chamada para **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Comentários  
 Se o aplicativo for executado em um sistema operacional de 64 bits, consulte [informações odbc de 64 bits](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
