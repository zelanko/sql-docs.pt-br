---
title: "A resposta é ODBC? | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 390188eb430e51bf0ce27bf2f32f9f82c195d4da
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="is-odbc-the-answer"></a>A resposta é ODBC?
Antes de investigar a questão de interoperabilidade, considere a seguinte pergunta: o aplicativo deve usar ODBC em todos os? Isso pode parecer uma pergunta estranha em um guia para ODBC, mas é, na verdade, uma legítima. ODBC não foi projetado para substituir completamente o banco de dados nativo APIs nem foi projetado para fornecer acesso de banco de dados em todas as circunstâncias. Ele foi projetado para fornecer uma interface comum para bancos de dados e foi planejado para liberar os programadores de aplicativos de ter que conhecer e manter os vínculos para vários bancos de dados.  
  
 Aplicativos personalizados são fortes candidatos para APIs de banco de dados nativo. O principal motivo é que aplicativos personalizados geralmente funcionam com um único DBMS e não precisa ser interoperável. Banco de dados nativo APIs pode fazer um trabalho melhor de ODBC de expor os recursos de um determinado DBMS e pode expor os recursos que não são expostos pelo ODBC. Além disso, como os desenvolvedores de aplicativos personalizados são geralmente familiarizados com o banco de dados nativo API para seu DBMS, é pouco motivo para aprender o ODBC. No entanto, é interessante observar que, para alguns DBMSs ODBC é a API de banco de dados nativo.  
  
 Portanto, quais aplicativos são candidatos para ODBC? Os melhores candidatos são aplicativos que funcionam com mais de um DBMS. Isso inclui praticamente todos os aplicativos genéricos e verticais. Ele também inclui um número de aplicativos personalizados. Por exemplo, aplicativos personalizados que usam vários DBMSs diferentes são muito mais fácil e limpeza de escrever com ODBC que com várias APIs nativas. E aplicativos personalizados criados com o ODBC são muito mais fácil de migrar uma empresa move de um DBMS para outro ou implanta o mesmo aplicativo contra DBMSs diferentes.
