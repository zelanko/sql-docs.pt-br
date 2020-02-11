---
title: Retornando SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2613593d9c2e20d5dfa01c0a0b4f9886dbc8e889
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057136"
---
# <a name="returning-sql_no_data"></a>Retornar SQL_NO_DATA
Quando um aplicativo *ODBC 2. x* workingwith um driver *ODBC 3. x* chama **SQLExecDirect**, **SQLExecute**ou **SQLParamData**e uma instrução UPDATE ou DELETE pesquisada foi executada, mas não afetou nenhuma linha na fonte de dados, o driver ODBC *3. x* deve retornar SQL_SUCCESS. Quando um aplicativo ODBC *3. x* que trabalha com um driver ODBC *3. x* chama **SQLExecDirect**, **SQLExecute**ou **SQLParamData** com o mesmo resultado, o driver ODBC *3. x* deve retornar SQL_NO_DATA.  
  
 Se uma instrução UPDATE ou DELETE pesquisada em um lote de instruções não afetar nenhuma linha na fonte de dados, **SQLMoreResults** retornará SQL_SUCCESS. Ele não pode retornar SQL_NO_DATA, porque isso significa que não há mais resultados, não que haja um resultado de uma atualização/exclusão pesquisada que não afetou nenhuma linha.
