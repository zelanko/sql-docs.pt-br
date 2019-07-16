---
title: Identificadores entre aspas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bc4d8378c243edf9f01cca58ff8be11d675711a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078999"
---
# <a name="quoted-identifiers"></a>Identificadores entre aspas
Em uma instrução SQL, os identificadores que contêm caracteres especiais ou palavras-chave de correspondência devem ser colocados entre *caracteres de aspas do identificador*; identificadores entre esses caracteres são conhecidos como *dentificadores*(também conhecido como *identificadores delimitados* em SQL-92). Por exemplo, o identificador de contas a pagar é citado no seguinte **selecionar** instrução:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 O motivo para delimitar identificadores é tornar a instrução pode ser analisado. Por exemplo, se as contas a pagar não foi citada na instrução anterior, o analisador seria supor que havia duas tabelas, contas e a pagar e retornar um erro de sintaxe que não eram separados por vírgula. O caractere de aspas do identificador é específica do driver e é recuperado com a opção SQL_IDENTIFIER_QUOTE_CHAR na **SQLGetInfo**. As listas de caracteres especiais e palavras-chave são recuperadas com as opções SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS na **SQLGetInfo**.  
  
 Para estar seguro, aplicativos interoperáveis geralmente citar todos os identificadores, exceto aqueles para pseudo colunas, como a coluna ROWID no Oracle. **SQLSpecialColumns** retorna uma lista de pseudo colunas. Além disso, se houver restrições específicas do aplicativo no qual os caracteres especiais podem aparecer em um nome de objeto, é melhor para aplicativos interoperáveis para não usar caracteres especiais em desses posições.
