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
manager: craigg
ms.openlocfilehash: 5af98bd8f16d7278b932ad89f1c81c58ddb1fb54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612198"
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
