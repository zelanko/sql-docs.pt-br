---
title: DEFINIR Comando EXACT | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300866"
---
# <a name="set-exact-command"></a>Comando SET EXACT
Especifica as regras para comparar duas seqüências de comprimentos diferentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 Especifica que as expressões devem corresponder ao caractere para que o caractere seja equivalente. Quaisquer espaços em branco nas expressões são ignorados para a comparação. Para a comparação, o mais curto das duas expressões é acolchoado à direita com espaços em branco para combinar com o comprimento da expressão mais longa.  
  
 OFF  
 (Padrão.) Especifica que, para ser equivalente, as expressões devem corresponder caractere para caractere até que o final da expressão no lado direito seja alcançado.  
  
## <a name="remarks"></a>Comentários  
 A configuração SET EXACT não tem efeito se ambas as cordas têm o mesmo comprimento.  
  
## <a name="string-comparisons"></a>Comparações de cordas  
 Visual FoxPro tem dois operadores relacionais que testam a igualdade.  
  
 O operador = realiza uma comparação entre dois valores do mesmo tipo. Este operador é adequado para comparar dados de caráter, numérico, data e lógica.  
  
 No entanto, quando você compara expressões de caracteres com o operador =, os resultados podem não ser exatamente o que você espera. As expressões de caracteres são comparadas de caráter para caractere da esquerda para a direita até que uma das expressões não seja igual à outra, até que o final da expressão no lado direito do operador = seja alcançado (SET EXACT OFF), ou até que as extremidades de ambas as expressões sejam alcançadas (SET EXACT ON).  
  
 O operador == pode ser usado quando uma comparação exata dos dados de caracteres é necessária. Se duas expressões de caracteres forem comparadas com o operador ==, as expressões em ambos os lados do operador == devem conter exatamente os mesmos caracteres, incluindo espaços em branco, para serem considerados iguais. A configuração SET EXACT é ignorada quando as seqüências de caracteres são comparadas usando ==.  
  
 A tabela a seguir mostra como a escolha do operador e a configuração SET EXACT afetam as comparações. (Um sublinhado representa um espaço em branco.)  
  
|Comparação|= EXACT OFF|= EXATO ON|== EXATO LIGADO OU DESLIGADO|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|Corresponder a|Corresponder a|Corresponder a|  
|"ab" = "abc"|Nenhuma correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"abc" = "ab"|Corresponder a|Nenhuma correspondência|Nenhuma correspondência|  
|"abc" = "ab_"|Nenhuma correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"ab" = "ab_"|Nenhuma correspondência|Corresponder a|Nenhuma correspondência|  
|"ab_" = "ab"|Corresponder a|Corresponder a|Nenhuma correspondência|  
|"" = "ab"|Nenhuma correspondência|Nenhuma correspondência|Nenhuma correspondência|  
|"ab" = ""|Corresponder a|Nenhuma correspondência|Nenhuma correspondência|  
|"__" = ""|Corresponder a|Corresponder a|Nenhuma correspondência|  
|"" = "___"|Nenhuma correspondência|Corresponder a|Nenhuma correspondência|  
|TRIM("___") = ""|Corresponder a|Corresponder a|Corresponder a|  
|"" = TRIM("___")|Corresponder a|Corresponder a|Corresponder a|  
  
## <a name="see-also"></a>Consulte Também  
 [Comando SET ANSI](../../odbc/microsoft/set-ansi-command.md)
