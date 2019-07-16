---
title: SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f899e7a034e1ec5fc967d834caad3a4ccc4caa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041835"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Quando um ODBC 3. *x* aplicativo chamará **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** em uma ODBC 2. *x* driver executar uma atualização pesquisada ou excluir a instrução que não afeta nenhuma linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou o ODBC 3. *x* aplicativo trabalhar com um ODBC 3. *x* chamadas de driver **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** com o mesmo resultado, o ODBC 3. *x* driver deve retornar SQL_NO_DATA.
