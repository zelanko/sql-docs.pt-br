---
description: Carregamento por ordinal
title: Carregando por ordinal | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb8929962e97e7560f50117218f621cd21846fc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429628"
---
# <a name="loading-by-ordinal"></a>Carregamento por ordinal
No ODBC *2. x*, o carregamento por ordinal pode ser executado para melhorar o desempenho do processo de conexão. Um driver ODBC *2. x* exporta uma função fictícia com o ordinal 199; Quando o Gerenciador de driver o detecta, ele resolve os endereços das funções ODBC por ordinal, não pelo nome. Essa funcionalidade ainda tem suporte para drivers ODBC *2. x* , mas não tem suporte para drivers ODBC *3. x* .
