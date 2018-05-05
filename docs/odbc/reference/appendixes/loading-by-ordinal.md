---
title: Carregando por Ordinal | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db3a9e517d70f19ad72e2991ca021013939a7db4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="loading-by-ordinal"></a>Carregamento por Ordinal
No ODBC 2. *x*, carregamento por ordinal pode ser realizado para melhorar o desempenho do processo de conexão. ODBC 2. *x* driver exporta uma função fictícia com o ordinal 199; quando o Gerenciador de Driver detecta a ele, ele resolve os endereços das funções ODBC por ordinal, não por nome. Ainda há suporte para essa funcionalidade do ODBC 2. *x* drivers, mas não há suporte para o ODBC 3 *. x* drivers.
