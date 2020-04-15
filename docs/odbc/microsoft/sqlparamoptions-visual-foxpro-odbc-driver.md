---
title: Opções SQLParam (Visual FoxPro ODBC Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd714ce7774265a2afd00d42894d644a516bc402
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299466"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 1  
  
 Permite que um aplicativo especifique vários valores para o conjunto de parâmetros atribuídos pelo [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). A capacidade de especificar múltiplos valores para um conjunto de parâmetros é útil para inserções em massa e outros trabalhos que exigem que a fonte de dados processe a mesma instrução SQL várias vezes com vários valores de parâmetros. Por exemplo, um aplicativo pode especificar três conjuntos de valores para o conjunto de parâmetros associados a uma instrução **INSERT** e, em seguida, executar a instrução **INSERT** uma vez para executar as três operações de inserção.  
  
 Para obter mais informações, consulte [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) no *Programador ODBC .*
