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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288087"
---
# <a name="is-odbc-the-answer"></a>O ODBC é a resposta?
Antes de se aprofundar na questão da interoperabilidade, considere a seguinte pergunta: A aplicação deve usar o ODBC em tudo? Esta pode parecer uma pergunta estranha a se fazer em um guia da ODBC, mas é, de fato, legítima. A ODBC não foi projetada para substituir completamente as APIs nativas do banco de dados, nem foi projetada para fornecer acesso ao banco de dados em todas as circunstâncias. Ele foi projetado para fornecer uma interface comum aos bancos de dados e foi destinado a libertar programadores de aplicativos de ter que aprender e manter links para vários bancos de dados.  
  
 Os aplicativos personalizados são os principais candidatos para APIs de banco de dados nativas. A principal razão é que os aplicativos personalizados geralmente funcionam com um único DBMS e não precisam ser interoperáveis. As APIs de banco de dados nativas podem fazer um trabalho melhor do que o ODBC de expor as capacidades de um DBMS específico e podem expor recursos não expostos pelo ODBC. Além disso, como os desenvolvedores de aplicativos personalizados geralmente estão familiarizados com a API de banco de dados nativo para seu DBMS, há pouca razão para aprender ODBC. No entanto, é interessante notar que para alguns DBMSs, o ODBC é a API de banco de dados nativo.  
  
 Então, quais candidaturas são candidatas à ODBC? Os melhores candidatos são aplicações que trabalham com mais de um DBMS. Isso inclui praticamente todas as aplicações genéricas e verticais. Ele também inclui uma série de aplicativos personalizados. Por exemplo, aplicativos personalizados que usam vários DBMSs diferentes são muito mais fáceis e limpos de gravar com ODBC do que com várias APIs nativas. E aplicativos personalizados escritos com ODBC são muito mais fáceis de migrar à medida que uma empresa passa de um DBMS para outro ou implanta o mesmo aplicativo contra DBMSs diferentes.
