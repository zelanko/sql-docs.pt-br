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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64bff8dcdd3802f75dc402c9ada60f82580aca5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288716"
---
# <a name="loading-by-ordinal"></a>Carregamento por ordinal
No ODBC *2.x,* o carregamento por ordinal poderia ser realizado para melhorar o desempenho do processo de conexão. Um driver ODBC *2.x* exporta uma função manequim com a ordinal 199; quando o Driver Manager detecta, ele resolve os endereços das funções ODBC por ordinal, não pelo nome. Essa funcionalidade ainda é suportada para drivers ODBC *2.x,* mas não é suportada para drivers ODBC *3.x.*
