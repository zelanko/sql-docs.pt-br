---
title: SQLBindCol (visual FoxPro ODBC Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindCol function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984d6605-39ba-4d33-ac94-22625bfa6107
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5eda58c6dec31206de9ddb10e73bdf90272d0a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300636"
---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível do núcleo  
  
 Atribui espaço de armazenamento a uma coluna de resultados e especifica o tipo do resultado. Quando [sqlFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ou [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md) é chamado, o driver coloca os dados para todas as colunas vinculadas nos locais atribuídos. Consulte [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) para obter o mapeamento entre os tipos de dados ODBC e Visual FoxPro.  
  
 Para obter mais informações, consulte [SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md) no *Programador ODBC*.
