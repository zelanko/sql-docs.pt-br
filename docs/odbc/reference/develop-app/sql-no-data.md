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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299786"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Quando um ODBC 3. *x* o aplicativo chama **SQLExecDirect,** **SQLExecute**ou **SQLParamData** em um ODBC 2. *x* driver para executar uma atualização pesquisada ou excluir declaração que não afete nenhuma linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou ODBC 3. *x* aplicação trabalhando com um ODBC 3. *x* driver chama **SQLExecDirect,** **SQLExecute**ou **SQLParamData** com o mesmo resultado, o ODBC 3. *x* motorista deve retornar SQL_NO_DATA.
