---
title: Comando SET ANSI | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d32e4dc27568b37f273ef654ebd45d26ca23e555
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997770"
---
# <a name="set-ansi-command"></a>Comando SET ANSI
Determina como as comparações entre cadeias de caracteres de comprimentos diferentes são feitas com o operador = em comandos SQL do Visual FoxPro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Padrão para o driver; o padrão para o Visual FoxPro é OFF). Preenche para que a cadeia de caracteres mais curta com os espaços em branco necessário torná-lo igual a mais cadeia de caracteres. As duas cadeias de caracteres serão então caractere comparado para caractere para seus comprimentos inteiros. Considere esta comparação:  
  
```  
'Tommy' = 'Tom'  
```  
  
 O resultado será False (. F.) se SET ANSI estiver on, porque quando preenchidas, 'Tom' torna-se 'Tom' e as cadeias de caracteres 'Tom' e 'Tommy' não corresponde ao caractere por caractere.  
  
 O = = operador usa esse método para comparações em comandos SQL do Visual FoxPro.  
  
 OFF  
 Especifica que a cadeia de caracteres mais curta não ser preenchido com espaços em branco. As duas cadeias de caracteres são comparadas caractere por caractere até o final da cadeia de caracteres mais curta for atingido. Considere esta comparação:  
  
```  
'Tommy' = 'Tom'  
```  
  
 O resultado será True (. T.) quando SET ANSI estiver desativado, porque a comparação para após 'Tom'.  
  
## <a name="remarks"></a>Comentários  
 SET ANSI determina se a mais curta das duas cadeias de caracteres é preenchida com espaços em branco quando uma comparação de cadeia de caracteres SQL é feita. SET ANSI não tem efeito sobre o operador; = = Quando você usa o operador = =, a cadeia de caracteres mais curta sempre é preenchida com espaços em branco para a comparação.  
  
## <a name="string-order"></a>Ordem de cadeia de caracteres  
 Em comandos SQL, a ordem da esquerda para a direita das duas cadeias de caracteres em uma comparação é irrelevantswitching uma cadeia de caracteres de um lado do = ou = = operador para o outro não afeta o resultado da comparação.  
  
## <a name="see-also"></a>Consulte também  
 [SELECT – comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [Comando SET EXACT](../../odbc/microsoft/set-exact-command.md)
