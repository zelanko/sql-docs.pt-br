---
description: Comando SET ANSI
title: Definir comando ANSI | Microsoft Docs
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
ms.openlocfilehash: 4a9f9c576199905c23994af4dc6b031114f4ad72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466398"
---
# <a name="set-ansi-command"></a>Comando SET ANSI
Determina como as comparações entre cadeias de caracteres de comprimentos diferentes são feitas com o operador = em comandos SQL do Visual FoxPro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 (O padrão para o driver; o padrão para o Visual FoxPro é desativado.) Preenche a cadeia de caracteres mais curta com os espaços em branco necessários para torná-lo igual ao comprimento da cadeia de caracteres mais longa. As duas cadeias de caracteres são então comparadas ao caractere para o caractere para seus comprimentos inteiros. Considere esta comparação:  
  
```  
'Tommy' = 'Tom'  
```  
  
 O resultado é false (. F.) se SET ANSI estiver on, porque quando preenchido, ' Tom ' se tornará ' Tom ' e as cadeias de caracteres ' Tom ' e ' Tommy ' não correspondem ao caractere para o caractere.  
  
 O operador = = usa esse método para comparações em comandos SQL do Visual FoxPro.  
  
 OFF  
 Especifica que a cadeia de caracteres menor não será preenchida com espaços em branco. As duas cadeias de caracteres são o caractere de comparação para o caractere até que o final da cadeia de caracteres mais curta seja atingido. Considere esta comparação:  
  
```  
'Tommy' = 'Tom'  
```  
  
 O resultado é true (. T.) quando SET ANSI é off, porque a comparação é interrompida após ' Tom '.  
  
## <a name="remarks"></a>Comentários  
 SET ANSI determina se a menor das duas cadeias de caracteres é preenchida com espaços em branco quando uma comparação de cadeia de caracteres SQL é feita. SET ANSI não tem nenhum efeito no operador = =; Quando você usa o operador = =, a cadeia de caracteres mais curta é sempre preenchida com espaços em branco para a comparação.  
  
## <a name="string-order"></a>Ordem da cadeia de caracteres  
 Em comandos SQL, a ordem da esquerda para a direita das duas cadeias de caracteres em uma comparação é irrelevantswitching uma cadeia de caracteres de um lado do operador = ou = = para a outra não afeta o resultado da comparação.  
  
## <a name="see-also"></a>Consulte Também  
 [SELECT-comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [Comando SET EXACT](../../odbc/microsoft/set-exact-command.md)
