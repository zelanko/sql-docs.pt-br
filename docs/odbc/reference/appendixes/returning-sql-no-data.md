---
title: Retornando SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0163c8e9d8c207d2ce8a7ae80c4ec03d9b7c64e2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="returning-sqlnodata"></a>Retornando SQL_NO_DATA
Quando um ODBC 2. *x* aplicativo trabalha com um ODBC 3*. x* driver chama **SQLExecDirect**, **SQLExecute**, ou **SQLParamData**, e uma atualização pesquisada ou uma instrução delete foi executada, mas não afetou linhas na fonte de dados, o ODBC 3*. x* driver deve retornar SQL_SUCCESS. Quando um ODBC 3*. x* aplicativo trabalhando com um ODBC 3*. x* driver chama **SQLExecDirect**, **SQLExecute**, ou  **SQLParamData** com o mesmo resultado, o ODBC 3*. x* driver deve retornar SQL_NO_DATA.  
  
 Se um pesquisada instrução update ou delete em um lote de instruções não afeta as linhas na fonte de dados, **SQLMoreResults** retorna SQL_SUCCESS. Ele não pode retornar SQL_NO_DATA, pois isso significaria que não há mais nenhum resultado, não que há é um resultado de uma atualização/exclusão pesquisada que não afetou linhas.
