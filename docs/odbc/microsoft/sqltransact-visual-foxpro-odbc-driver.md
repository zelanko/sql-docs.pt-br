---
description: SQLTransact (Driver ODBC do Visual FoxPro)
title: SQLTransact (driver ODBC do Visual FoxPro) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1deed379c456ba2f15d30b6783c95d657e688457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500109"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível de núcleo  
  
 Solicita uma operação de confirmação ou reversão para todas as operações ativas em todos os identificadores de instrução (*HSTMT*s) associados a uma conexão ou para todas as conexões associadas ao identificador de ambiente, *HENV*. **SQLTransact** funciona somente para fontes de dados que são [bancos](../../odbc/microsoft/visual-foxpro-terminology.md)de dado.  
  
 Se uma confirmação falhar quando estiver no modo manual, a transação permanecerá ativa; Você pode optar por reverter a transação ou tentar novamente a operação de confirmação. Se uma operação de confirmação falhar quando estiver no modo de transação automática, a transação será revertida automaticamente; a transação não pode ficar inativa.  
  
 Para obter mais informações, consulte [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) na *referência do programador de ODBC*.
