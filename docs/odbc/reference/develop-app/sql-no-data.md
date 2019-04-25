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
manager: craigg
ms.openlocfilehash: 749351694a41764b9b5cc8bf3421340d62626aaf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445958"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Quando um ODBC 3. *x* aplicativo chamará **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** em uma ODBC 2. *x* driver executar uma atualização pesquisada ou excluir a instrução que não afeta nenhuma linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou o ODBC 3. *x* aplicativo trabalhar com um ODBC 3. *x* chamadas de driver **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** com o mesmo resultado, o ODBC 3. *x* driver deve retornar SQL_NO_DATA.
