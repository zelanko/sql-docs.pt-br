---
title: SQLTransact (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bed779e7c6d0e49674dcf2753ccd64c7f4624347
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 ODBC API conformidade: Nível de núcleo  
  
 Solicita uma operação de confirmação ou reversão de todas as operações ativas em todos os identificadores de instrução (*hstmt*s) associado com uma conexão ou para todas as conexões associadas com o identificador de ambiente, *henv*. **SQLTransact** funciona apenas para fontes de dados que são [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Se uma confirmação falhar no modo manual, a transação permanecerá ativa; Você pode escolher reverter a transação ou repita a operação de confirmação. Se uma operação de confirmação falhar no modo de transação automática, a transação é revertida automaticamente. a transação não pode estar inativa.  
  
 Para obter mais informações, consulte [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) no *referência do programador de ODBC*.
