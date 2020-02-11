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
ms.openlocfilehash: 2e325793a7b703c445be836f6f427645acda3370
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138846"
---
# <a name="is-odbc-the-answer"></a>O ODBC é a resposta?
Antes de se aprofundar na pergunta da interoperabilidade, considere a seguinte pergunta: se o aplicativo usa ODBC? Isso pode parecer uma pergunta estranha de fazer um guia para o ODBC, mas é, na verdade, um legítimo. O ODBC não foi projetado para substituir completamente as APIs do banco de dados nativo, nem foi projetado para fornecer acesso ao banco de dados em todas as circunstâncias. Ele foi projetado para fornecer uma interface comum aos bancos de dados e foi destinado a liberar programadores de aplicativos de ter que aprender e manter links para vários bancos de dados.  
  
 Aplicativos personalizados são candidatos principais para APIs de banco de dados nativo. O principal motivo é que os aplicativos personalizados geralmente funcionam com um único DBMS e não precisam ser interoperáveis. APIs de banco de dados nativo podem fazer um trabalho melhor do que o ODBC, expondo os recursos de um determinado DBMS e podem expor recursos não expostos pelo ODBC. Além disso, como os desenvolvedores de aplicativos personalizados geralmente estão familiarizados com a API de banco de dados nativa para seu DBMS, há pouco motivo para aprender o ODBC. No entanto, é interessante observar que, para alguns DBMSs, o ODBC é a API de banco de dados nativa.  
  
 Quais aplicativos são candidatos ao ODBC? Os melhores candidatos são aplicativos que funcionam com mais de um DBMS. Isso inclui praticamente todos os aplicativos genéricos e verticais. Ele também inclui vários aplicativos personalizados. Por exemplo, aplicativos personalizados que usam vários DBMSs diferentes são muito mais fáceis e mais simples de escrever com o ODBC do que com várias APIs nativas. E aplicativos personalizados escritos com o ODBC são muito mais fáceis de migrar, uma vez que uma empresa passa de um DBMS para outro ou implanta o mesmo aplicativo em DBMSs diferentes.
