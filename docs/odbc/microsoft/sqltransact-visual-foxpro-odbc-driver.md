---
title: SQLTransact (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e554a8669b6e6e95e234a5b939477a8bb2f7b8cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948862"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível de núcleo  
  
 Solicita uma operação de confirmação ou reversão para todas as operações ativas em todos os identificadores de instrução (*hstmt*s) associado com uma conexão ou para todas as conexões associadas com o identificador de ambiente *henv*. **SQLTransact** funciona apenas para fontes de dados que são [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Se uma confirmação falhar no modo manual, a transação permanecerá ativa; Você pode escolher reverter a transação ou repita a operação de confirmação. Se uma operação de confirmação falhar no modo de transação automática, a transação é revertida automaticamente. a transação não pode ficar inativa.  
  
 Para obter mais informações, consulte [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) na *referência do programador de ODBC*.
