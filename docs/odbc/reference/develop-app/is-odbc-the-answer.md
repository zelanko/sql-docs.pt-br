---
title: O ODBC é a resposta? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f90f2395eac5dce76848d7bc309f1a3d5ce289f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600554"
---
# <a name="is-odbc-the-answer"></a>O ODBC é a resposta?
Antes de investigar a questão de interoperabilidade, considere a seguinte pergunta: o aplicativo deve usar ODBC em todos os? Isso pode parecer uma estranha pergunta a ser feita em um guia para ODBC, mas é, na verdade, uma legítima. ODBC não foi projetado para substituir completamente os APIs de banco de dados nativa, nem foi projetado para fornecer acesso de banco de dados em todas as circunstâncias. Ele foi projetado para fornecer uma interface comum para bancos de dados e foi destinado para liberar os programadores de aplicativos precise conhecer e manter os links para vários bancos de dados.  
  
 Aplicativos personalizados são candidatos ideais para APIs de banco de dados nativo. O principal motivo é que os aplicativos personalizados geralmente funcionam com um DBMS único e não precisa ser interoperável. Banco de dados nativo APIs pode fazer um trabalho melhor que o ODBC de expor os recursos de um DBMS específico e pode expor recursos não são expostos pelo ODBC. Além disso, como os desenvolvedores de aplicativos personalizados são geralmente familiarizados com o banco de dados nativo API para seu DBMS, há poucos motivos para aprender o ODBC. No entanto, é interessante observar que, para alguns DBMSs, o ODBC é a API de banco de dados nativo.  
  
 Então, quais aplicativos são candidatos para ODBC? Os melhores candidatos são aplicativos que funcionam com mais de um DBMS. Isso inclui praticamente todos os aplicativos genéricos e verticais. Ele também inclui um número de aplicativos personalizados. Por exemplo, aplicativos personalizados que usam vários DBMSs diferentes são muito mais fácil e limpo para gravar com o ODBC que com as várias APIs nativas. E aplicativos personalizados escritos com o ODBC são muito mais fácil de migrar, conforme se move de um DBMS para outro de uma empresa ou implanta o mesmo aplicativo em relação a diferentes DBMSs.
