---
title: Comando exato conjunto | Microsoft Docs
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
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6f5576ec5a1275914ee0558cf3fcd151ee3c3cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904651"
---
# <a name="set-exact-command"></a>Comando exato do conjunto
Especifica as regras para comparar duas cadeias de caracteres de comprimentos diferentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que expressões devem coincidir com o caractere a ser equivalentes. Todos os espaços em branco nas expressões são ignorados para a comparação. Para a comparação, a menor das duas expressões é preenchido à direita com espaços em branco para corresponder ao comprimento da expressão maior.  
  
 OFF  
 (Padrão). Especifica que, para que seja equivalente, expressões devem corresponder caractere até que seja atingido o fim da expressão no lado direito.  
  
## <a name="remarks"></a>Remarks  
 A configuração definida exata não terá efeito se duas cadeias de caracteres são o mesmo comprimento.  
  
## <a name="string-comparisons"></a>Comparações de cadeia de caracteres  
 Do Visual FoxPro tem dois operadores relacionais que o teste de igualdade.  
  
 O = operador executa uma comparação entre dois valores do mesmo tipo. Esse operador é adequado para comparação de caracteres, numérico, data e dados lógicos.  
  
 No entanto, ao comparar expressões de caractere com o operador =, os resultados podem não ser exatamente o que você espera. Expressões de caractere são comparadas caractere por caractere da esquerda para a direita até que uma das expressões não é igual ao outro, até o fim da expressão no lado direito do = operador for atingido (SET exata OFF), ou até que as extremidades de ambas as expressões são atingido (SET EXACT ON).  
  
 O = = operador pode ser usado quando uma comparação exata dos dados de caracteres é necessária. Se duas expressões de caracteres são comparadas com o operador = =, as expressões em ambos os lados do = = operador deve conter exatamente os mesmos caracteres, incluindo espaços em branco, a ser considerados iguais. O conjunto exato será ignorada quando as cadeias de caracteres são comparadas usando = =.  
  
 A tabela a seguir mostra como a escolha de operador e a configuração SET EXACT afetam comparações. (Um sublinhado representa um espaço em branco.)  
  
|Comparação|= EXATO DESATIVADO|= EXATO EM|= = EXATO ON ou OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|Correspondência|Correspondência|Correspondência|  
|"ab" = "abc"|Nenhuma correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"abc" = "ab"|Correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"abc" = "ab_"|Nenhuma correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"ab" = "ab_"|Nenhuma correspondência|Correspondência|Nenhuma correspondência|  
|"ab_" = "ab"|Correspondência|Correspondência|Nenhuma correspondência|  
|"" = "ab"|Nenhuma correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"ab" = ""|Correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"__" = ""|Correspondência|Correspondência|Nenhuma correspondência|  
|"" = "___"|Nenhuma correspondência|Correspondência|Nenhuma correspondência|  
|TRIM("___") = ""|Correspondência|Correspondência|Correspondência|  
|"" = TRIM("___")|Correspondência|Correspondência|Correspondência|  
  
## <a name="see-also"></a>Consulte também  
 [Comando SET ANSI](../../odbc/microsoft/set-ansi-command.md)
