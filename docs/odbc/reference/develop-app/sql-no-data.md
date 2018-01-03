---
title: SQL_NO_DATA | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da9e5ffc19d884d2cb182190e11ba4dcf0a915bd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Quando um ODBC 3. *x* aplicativo chama **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** em um ODBC 2. *x* driver para executar uma atualização pesquisada ou delete que não afeta qualquer linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou ODBC 3. *x* aplicativo trabalhando com um ODBC 3. *x* driver chama **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** com o mesmo resultado, o ODBC 3. *x* driver deve retornar SQL_NO_DATA.
