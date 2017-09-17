---
title: Identificadores entre aspas | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07a0c8299fc4063e72353025465309c426a3a251
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="quoted-identifiers"></a>Identificadores entre aspas
Em uma instrução SQL, os identificadores que contêm caracteres especiais ou correspondência de palavras-chave devem ser colocados entre *caracteres de aspas*; identificadores entre esses caracteres são conhecidos como *deidentificadoresentreaspas*(também conhecido como *identificadores delimitados* em SQL-92). Por exemplo, o identificador de contas a pagar é mencionado na tabela a seguir **selecione** instrução:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 O motivo para delimitar identificadores é fazer a instrução pode ser analisado. Por exemplo, se contas a pagar não estava entre aspas na instrução anterior, o analisador seria assumir duas tabelas, contas e a pagar e retornar um erro de sintaxe que não eram separados por uma vírgula. O identificador de caractere de aspas é específico do driver e é recuperado com a opção SQL_IDENTIFIER_QUOTE_CHAR na **SQLGetInfo**. A lista de caracteres especiais e palavras-chave é recuperada com as opções SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS na **SQLGetInfo**.  
  
 Para ser seguro, aplicativos interoperáveis geralmente cotação todos os identificadores, exceto aqueles para pseudo colunas, como a coluna ROWID no Oracle. **SQLSpecialColumns** retorna uma lista de pseudo colunas. Além disso, se houver restrições específicas do aplicativo no qual os caracteres especiais podem aparecer em um nome de objeto, ele é ideal para aplicativos interoperáveis para não usar caracteres especiais em posições desses.
