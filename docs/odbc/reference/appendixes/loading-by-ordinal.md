---
title: Carregamento por Ordinal | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 702e1fe58080cc370ab9a858c985a7744df85050
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845854"
---
# <a name="loading-by-ordinal"></a>Carregamento por ordinal
No ODBC 2. *x*, carregamento por ordinal pôde ser executado para melhorar o desempenho do processo de conexão. ODBC 2. *x* driver exporta uma função fictícia com o ordinal 199; quando o Gerenciador de Driver detecta a ele, ele resolve os endereços das funções ODBC por ordinal, e não por nome. Ainda há suporte para essa funcionalidade para o ODBC 2. *x* drivers, mas não há suporte para ODBC 3 *. x* drivers.
