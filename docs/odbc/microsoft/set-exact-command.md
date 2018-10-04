---
title: Comando SET EXACT | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16651df836ac3fb87c5e28b4b8fa25088e9dd86a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606795"
---
# <a name="set-exact-command"></a>Comando SET EXACT
Especifica as regras para comparar duas cadeias de caracteres de comprimentos diferentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que as expressões devem corresponder ao caractere ser equivalentes. Quaisquer espaços em branco nas expressões são ignorados para a comparação. Para comparação, a mais curta das duas expressões será preenchida à direita com espaços em branco para corresponder ao comprimento da expressão maior.  
  
 OFF  
 (Padrão). Especifica que, para serem equivalentes, expressões devem corresponder ao caractere até o final da expressão no lado direito for atingido.  
  
## <a name="remarks"></a>Comentários  
 A configuração de SET EXACT não tem nenhum efeito se duas cadeias de caracteres têm o mesmo comprimento.  
  
## <a name="string-comparisons"></a>Comparações de cadeia de caracteres  
 Do Visual FoxPro tem dois operadores relacionais que testam a igualdade.  
  
 O = operador executa uma comparação entre dois valores do mesmo tipo. Esse operador é adequado para comparar dados de caracteres, numérico, data e lógicos.  
  
 No entanto, ao comparar expressões de caractere com o operador =, os resultados podem não ser exatamente o que você espera. Expressões de caracteres são comparadas caractere por caractere da esquerda para a direita até que uma das expressões não é igual ao outro, até o final da expressão no lado direito do = operador seja atingido (SET EXACT OFF), ou até que as extremidades de ambas as expressões são atingido (SET EXACT ON).  
  
 O = = operador pode ser usado quando uma comparação exata dos dados de caracteres é necessária. Se duas expressões de caracteres são comparadas com o operador = =, as expressões em ambos os lados do = = operador deve conter exatamente os mesmos caracteres, incluindo espaços em branco, a serem considerados iguais. A configuração de SET EXACT é ignorada quando as cadeias de caracteres são comparadas usando = =.  
  
 A tabela a seguir mostra como a escolha do operador e a configuração de SET EXACT afetam as comparações. (Um sublinhado representa um espaço em branco.)  
  
|Comparação|= EXATO DESATIVADO|= ON EXATO|= = EXATO como ON ou OFF|  
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
