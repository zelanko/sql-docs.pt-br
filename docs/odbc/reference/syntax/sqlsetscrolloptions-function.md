---
title: Função SQLSetScrollOptions | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79ab0c408748fcbea30fdc2c792e433db8a4309d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-function"></a>Função SQLSetScrollOptions
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: Deprecated  
  
 **Resumo**  
 Em ODBC 3 *. x*, a função ODBC 2.0 **SQLSetScrollOptions** foi substituído por chamadas para **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 2 *. x* aplicativo estiver trabalhando com um ODBC 3 *. x* driver, consulte [mapeamento preterido funções](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
> [!NOTE]  
>  Quando o Gerenciador de Driver mapeia **SQLSetScrollOptions** para um aplicativo trabalhando com um ODBC 3 *. x* driver não oferece suporte a **SQLSetScrollOptions**, o Driver Manager define a opção de instrução SQL_ROWSET_SIZE, não o atributo SQL_ATTR_ROW_ARRAY_SIZE instrução para o *RowsetSize* argumento **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** não pode ser usado por um aplicativo ao buscar várias linhas por uma chamada para **SQLFetch** ou **SQLFetchScroll**. Ele pode ser usado somente quando a busca de várias linhas por uma chamada para **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Remarks  
 Se o aplicativo será executado em um sistema operacional de 64 bits, consulte [informações de ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
