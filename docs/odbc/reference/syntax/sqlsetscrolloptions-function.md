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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342944"
---
# <a name="sqlsetscrolloptions-function"></a>Função SQLSetScrollOptions
**Conformidade**  
 Versão introduzida: Conformidade com os padrões do ODBC 1,0: Preterido  
  
 **Resumo**  
 No ODBC *3. x*, a função **SQLSetScrollOptions** do ODBC 2,0 foi substituída por chamadas para **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um aplicativo ODBC *2. x* está trabalhando com um driver ODBC *3. x* , consulte [mapeando funções](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) preteridas no apêndice G: Diretrizes de driver para compatibilidade com versões anteriores.  
> 
> [!NOTE]
>  Quando o Gerenciador de driver mapeia o **SQLSetScrollOptions** para um aplicativo que trabalha com um driver ODBC *3. x* que não dá suporte a **SQLSetScrollOptions**, o Gerenciador de driver define a opção de instrução SQL_ROWSET_SIZE, não a SQL_ATTR_ROW_ Atributo de instrução ARRAY_SIZE, para o argumento de *conjunto* em **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para SQLFetch ou **SQLFetchScroll**. Ele pode ser usado somente ao buscar várias linhas por uma chamada para **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Comentários  
 Se seu aplicativo for executado em um sistema operacional de 64 bits, confira [informações ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
