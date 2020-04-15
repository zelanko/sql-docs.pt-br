---
title: DEFINIR Comando ANSI | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97269642b4147b966fdd71003f5f81ebe7905282
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300906"
---
# <a name="set-ansi-command"></a>Comando SET ANSI
Determina como as comparações entre seqüências de diferentes comprimentos são feitas com o operador = nos comandos Visual FoxPro SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 (Padrão para o driver; o padrão para Visual FoxPro é OFF.) Pads a corda mais curta com os espaços em branco necessários para torná-lo igual ao comprimento da corda mais longa. As duas cordas são então comparadas personagem por personagem para todos os seus comprimentos. Considere esta comparação:  
  
```  
'Tommy' = 'Tom'  
```  
  
 O resultado é Falso (. F.) se SET ANSI está ligado, porque quando acolchoado, 'Tom' se torna 'Tom ' e as cordas 'Tom ' e 'Tommy' não combinam personagem para personagem.  
  
 O operador == usa este método para comparações nos comandos Visual FoxPro SQL.  
  
 OFF  
 Especifica que a seqüência mais curta não deve ser acolchoada com espaços em branco. As duas cordas são comparadas personagem por personagem até que o final da seqüência mais curta seja alcançado. Considere esta comparação:  
  
```  
'Tommy' = 'Tom'  
```  
  
 O resultado é True (. T.) quando set ANSI está desligado, porque a comparação pára após 'Tom'.  
  
## <a name="remarks"></a>Comentários  
 SET ANSI determina se o menor de duas strings é acolchoado com espaços em branco quando uma comparação de string SQL é feita. CONJUNTO ANSI não tem efeito sobre o operador == ; quando você usa o operador ==, a seqüência mais curta é sempre acolchoada com espaços em branco para a comparação.  
  
## <a name="string-order"></a>Ordem das cordas  
 Nos comandos SQL, a ordem da esquerda para a direita das duas strings em uma comparação é irrelevante mudar uma seqüência de um lado do operador = ou == para o outro não afeta o resultado da comparação.  
  
## <a name="see-also"></a>Consulte Também  
 [SELECT - Comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [Comando SET EXACT](../../odbc/microsoft/set-exact-command.md)
