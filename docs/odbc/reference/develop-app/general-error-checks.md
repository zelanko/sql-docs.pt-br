---
title: Verificações gerais de erros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35dc509e0bda51c8d219b76f48b44b2b03dba8cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305557"
---
# <a name="general-error-checks"></a>Verificações de erro gerais
O Driver Manager verifica um erro geral. Ele sempre retorna SQL_ERROR quando encontra o seguinte erro: A função deve ser suportada pelo motorista.
