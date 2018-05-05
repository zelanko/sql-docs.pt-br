---
title: SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff7ba5184642f419a62ffef0610bfc08995ed6b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Quando um ODBC 3. *x* aplicativo chama **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** em um ODBC 2. *x* driver para executar uma atualização pesquisada ou delete que não afeta qualquer linha na fonte de dados, o driver deve retornar SQL_SUCCESS, não SQL_NO_DATA. Quando um ODBC 2. *x* ou ODBC 3. *x* aplicativo trabalhando com um ODBC 3. *x* driver chama **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** com o mesmo resultado, o ODBC 3. *x* driver deve retornar SQL_NO_DATA.
