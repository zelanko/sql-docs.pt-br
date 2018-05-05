---
title: Limitações de nome de tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c33928107e3094e0e2116170b79352268ec9964
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="table-name-limitations"></a>Limitações de nome de tabela
Nomes de tabela podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes de tabela contiverem qualquer caractere, exceto letras, números e sublinhados, o nome deve ser delimitado colocando-o entre aspas back (').  
  
 Quando o driver do Microsoft Excel é usado, e um nome de tabela não é qualificado por uma referência de banco de dados, o banco de dados padrão é implícita. Se um nome no Microsoft Excel inclui o "!" caractere, ele automaticamente será convertido para o caractere "$" em vez disso.  
  
 O nome de tabela do Microsoft Excel que faz referência a \<filename > há suporte para o Microsoft Excel 3.0 e 4.0 arquivos. O nome de tabela do Microsoft Excel que faz referência a \<nome de pasta de trabalho > há suporte para arquivos do Microsoft Excel 5.0, 7.0 ou 97.  
  
 Quando o driver dBASE é usado, os caracteres com um valor ASCII maior do que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Access for usado, o nome da tabela é limitado a 64 caracteres.  
  
 Quando o driver do Microsoft Excel 3.0 ou 4.0, Paradox ou texto dBASE é usado, especiais MS-DOS palavras-chave CON, AUX, LPT1, LPT2 não devem ser usadas como nomes de tabela.
