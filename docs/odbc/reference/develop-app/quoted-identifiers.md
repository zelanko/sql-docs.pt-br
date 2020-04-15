---
title: Identificadores citados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281999"
---
# <a name="quoted-identifiers"></a>Identificadores entre aspas
Em uma declaração SQL, os identificadores que contenham caracteres especiais ou palavras-chave de correspondência devem ser incluídos em *caracteres de citação identificador;* identificadores incluídos em tais caracteres são conhecidos como *identificadores citados* (também conhecidos como *identificadores delimitados* no SQL-92). Por exemplo, o identificador contas a pagar é citado na seguinte declaração **SELECT:**  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 A razão para citar identificadores é tornar a declaração parseable. Por exemplo, se as contas a pagar não foram citadas na declaração anterior, o analisador assumiria que havia duas tabelas, contas e a pagar, e devolveria um erro de sintaxe que eles não foram separados por uma coma. O caractere de citação do identificador é específico do driver e é recuperado com a opção SQL_IDENTIFIER_QUOTE_CHAR no **SQLGetInfo**. As listas de caracteres especiais e de palavras-chave são recuperadas com as opções SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS no **SQLGetInfo**.  
  
 Para ser seguro, aplicativos interoperáveis frequentemente citam todos os identificadores, exceto aqueles para pseudo-colunas, como a coluna ROWID no Oracle. **SQLSpecialColumns** retorna uma lista de pseudo-colunas. Além disso, se houver restrições específicas de aplicativos sobre onde caracteres especiais podem aparecer em um nome de objeto, é melhor que aplicativos interoperáveis não usem caracteres especiais nessas posições.
