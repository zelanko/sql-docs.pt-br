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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287257"
---
# <a name="sqlsetscrolloptions-function"></a>Função SQLSetScrollOptions
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: preterida  
  
 **Resumo**  
 No ODBC *3. x*, a função **SQLSetScrollOptions** do ODBC 2,0 foi substituída por chamadas para **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC *2. x* está trabalhando com um driver ODBC *3. x* , consulte [mapeando funções preteridas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
> 
> [!NOTE]
>  Quando o Gerenciador de driver mapeia o **SQLSetScrollOptions** para um aplicativo que trabalha com um driver ODBC *3. x* que não dá suporte a **SQLSetScrollOptions**, o Gerenciador de Driver define a opção de instrução SQL_ROWSET_SIZE, não o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE, para o argumento de *conjunto* em **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente ao buscar várias linhas por uma chamada para **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Comentários  
 Se seu aplicativo for executado em um sistema operacional de 64 bits, confira [informações ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
