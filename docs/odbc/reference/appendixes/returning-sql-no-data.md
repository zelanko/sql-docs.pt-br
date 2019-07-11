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
manager: craigg
ms.openlocfilehash: e2f731589dcbc10d24ff42d895db60f9f8c054de
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794177"
---
# <a name="returning-sqlnodata"></a>Retornar SQL_NO_DATA
Quando um ODBC *2.x* aplicativo se trabalha com um ODBC *3.x* driver chama **SQLExecDirect**, **SQLExecute**, ou  **SQLParamData**, e uma instrução de exclusão ou atualização pesquisada foi executada, mas não afetou nenhuma linha na fonte de dados, o ODBC *3.x* driver deve retornar SQL_SUCCESS. Quando um ODBC *3.x* aplicativo trabalhar com ODBC *3.x* driver chama **SQLExecDirect**, **SQLExecute**, ou  **SQLParamData** com o mesmo resultado, o ODBC *3.x* driver deve retornar SQL_NO_DATA.  
  
 Se um pesquisada instrução update ou delete em um lote de instruções não afetará quaisquer linhas na fonte de dados, **SQLMoreResults** retorna SQL_SUCCESS. Ele não pode retornar SQL_NO_DATA, porque isso significaria que não há mais nenhum resultado, não que existe é um resultado de uma atualização/exclusão pesquisada que não afetou linhas.
