---
title: Verificações de transição de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299701"
---
# <a name="state-transition-checks"></a>Verificações de transição de estado
O Gerenciador de driver verifica se o estado do ambiente, da conexão ou da instrução é apropriado para a função que está sendo chamada. Por exemplo, uma conexão deve estar em um estado alocado quando **SQLConnect** for chamado; uma instrução deve estar em um estado preparado quando **SQLExecute** é chamado. O Gerenciador de driver retorna SQL_ERROR para erros de transição de estado.
