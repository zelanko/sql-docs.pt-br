---
title: Suporte para o modelo de Cursor (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13f8c22a9c47fd4e0d83fdb7bb73ff12f8e96e93
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modelo de Cursor com suporte (Driver ODBC do Visual FoxPro)
O Driver de ODBC do Visual FoxPro oferece suporte a *bloco* (*linhas*) e *estático* cursores. Cursores estáticos são suportados para qualquer driver compatível com conformidade de nível 1 ODBC. O driver não dá suporte a dinâmicos, controlados por conjunto de chaves ou misto (conjunto de chaves e dinâmico) cursores.  
  
 O aplicativo pode chamar [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) com uma opção de SQL_CURSOR_TYPE de SQL_CURSOR_FORWARD_ONLY (cursor em bloco) ou SQL_CURSOR_STATIC (cursor estático).  
  
> [!NOTE]  
>  Se você chamar **SQLSetStmtOption** com uma opção de SQL_CURSOR_TYPE diferente SQL_CURSOR_FORWARD_ONLY ou SQL_CURSOR_STATIC, a função retorna SQL_SUCCESS_WITH_INFO com um SQLSTATE de 01S02 (valor da opção alterado). O driver define todos os modos de cursor sem suporte para SQL_CURSOR_STATIC.  
  
 Para obter mais informações sobre tipos de cursor e sobre **SQLSetStmtOption**, consulte o [referência do programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursor em bloco  
 Um conjunto de resultados de rolagem de avanço, somente leitura retornado ao cliente, que é responsável por manter o armazenamento de dados.  
  
## <a name="static-cursor"></a>cursor estático  
 Um instantâneo de um conjunto de dados definido pela consulta. Cursores estáticos não refletem as alterações em tempo real dos dados subjacentes por outros usuários. O buffer de memória do cursor é mantido pela biblioteca de cursores ODBC, que permite rolagem para frente e para trás.  
  
## <a name="rowset"></a>conjunto de linhas  
 Blocos de dados armazenados em um cursor, que representa a linhas recuperadas da fonte de dados.
