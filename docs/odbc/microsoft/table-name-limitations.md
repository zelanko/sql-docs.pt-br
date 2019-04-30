---
title: Limitações de nome de tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31c1703bc03a2881e7b9b96989b8949cc81aba7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226339"
---
# <a name="table-name-limitations"></a>Limitações de nome de tabela
Nomes de tabela podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes de tabela contiverem quaisquer caracteres, exceto letras, números e sublinhados, o nome deve ser delimitado, colocando-o no back-aspas (').  
  
 Quando o driver do Microsoft Excel for usado, e um nome de tabela não é qualificado por uma referência de banco de dados, o banco de dados padrão é implícito. Se um nome no Microsoft Excel inclui a "!" caractere, ele automaticamente será convertido para o caractere "$" em vez disso.  
  
 O nome de tabela do Microsoft Excel que faz referência a \<filename > tem suporte para Microsoft Excel 3.0 e 4.0 arquivos. O nome de tabela do Microsoft Excel que faz referência a \<nome de pasta de trabalho > há suporte para arquivos do Microsoft Excel 97, 7.0 ou 5.0.  
  
 Quando o driver do dBASE é usado, os caracteres com um valor de ASCII maior do que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Access for usado, o nome da tabela é limitado a 64 caracteres.  
  
 Quando o driver do dBASE, Microsoft Excel 3.0 ou 4.0, Paradox, ou o texto é usado, o MS-DOS palavras-chave especiais CON, AUX, LPT1 e LPT2 não devem ser usadas como nomes de tabela.
