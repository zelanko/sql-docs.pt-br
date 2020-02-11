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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041835"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Quando um ODBC 3. *x* o aplicativo chama **SQLExecDirect**, **SQLExecute**ou **SQLParamData** em um ODBC 2. *x* para executar uma atualização pesquisada ou uma instrução DELETE que não afete nenhuma linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou ODBC 3. *x* aplicativo trabalhando com um ODBC 3. o driver *x* chama **SQLExecDirect**, **SQLExecute**ou **SQLPARAMDATA** com o mesmo resultado, o ODBC 3. o driver *x* deve retornar SQL_NO_DATA.
