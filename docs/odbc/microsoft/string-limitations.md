---
title: Limitações de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948768"
---
# <a name="string-limitations"></a>Limitações de cadeia de caracteres
O comprimento máximo de uma cadeia de caracteres de instrução SQL é de 65.000 caracteres.  
  
 Quando o driver do Microsoft Access é usado, somente as constantes de cadeia de caracteres SQL-92 (com aspas simples, não aspas duplas) têm suporte.  
  
 O caractere de barra vertical (&#124;) não pode ser usado em uma cadeia de caracteres, independentemente de o caractere ser colocado entre aspas de fundo ou não.  
  
 Para a interoperabilidade máxima, os aplicativos devem passar cadeias de caracteres em parâmetros em vez de passar cadeias de caracteres entre aspas.
