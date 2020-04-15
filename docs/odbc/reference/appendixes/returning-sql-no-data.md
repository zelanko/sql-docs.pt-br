---
title: Voltando SQL_NO_DATA | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2c806edd5d5647e09c00975ad7207ee5c2c876
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305107"
---
# <a name="returning-sql_no_data"></a>Retornar SQL_NO_DATA
Quando um aplicativo ODBC *2.x* funcionando com um driver ODBC *3.x* chama **SQLExecDirect,** **SQLExecute**ou **SQLParamData,** e uma declaração de atualização ou exclusão pesquisada foi executada, mas não afetou nenhuma linha na fonte de dados, o driver ODBC *3.x* deve retornar SQL_SUCCESS. Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *3.x* chama **SQLExecDirect,** **SQLExecute**ou **SQLParamData** com o mesmo resultado, o driver ODBC *3.x* deve retornar SQL_NO_DATA.  
  
 Se uma instrução de atualização ou exclusão pesquisada em um lote de declarações não afetar nenhuma linha na fonte de dados, o **SQLMoreResults** retorna SQL_SUCCESS. Ele não pode retornar SQL_NO_DATA, porque isso significaria que não há mais resultados, não que haja um resultado de uma atualização/exclusão pesquisada que não afetou nenhuma linha.
