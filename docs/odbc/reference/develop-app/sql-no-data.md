---
description: SQL_NO_DATA
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
ms.openlocfilehash: eb81d6f1fce50a27aba203eec4b78648754010e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424568"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Quando um ODBC 3. *x* o aplicativo chama **SQLExecDirect**, **SQLExecute**ou **SQLParamData** em um ODBC 2. *x* para executar uma atualização pesquisada ou uma instrução DELETE que não afete nenhuma linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou ODBC 3. *x* aplicativo trabalhando com um ODBC 3. o driver *x* chama **SQLExecDirect**, **SQLExecute**ou **SQLPARAMDATA** com o mesmo resultado, o ODBC 3. o driver *x* deve retornar SQL_NO_DATA.
