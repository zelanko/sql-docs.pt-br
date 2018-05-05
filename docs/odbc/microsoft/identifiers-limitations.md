---
title: Limitações de identificadores | Microsoft Docs
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 087d7ba056a5da10ae8d191592f06c312583b62b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-limitations"></a>Limitações de identificadores
Se um identificador contiver um espaço ou um símbolo especial, o identificador deve ser colocado entre aspas voltar. Um nome válido é uma cadeia de caracteres de não mais do que 64 caracteres, dos quais o primeiro caractere não deve ser um espaço. Os nomes válidos não podem incluir caracteres de controle ou os seguintes caracteres especiais: ' &#124; # *? [ ] . ! $ .  
  
 Não use palavras reservadas listadas na gramática SQL no Apêndice C do *referência do programador de ODBC* (ou a forma abreviada dessas palavras reservadas) como identificadores (ou seja, nomes tabela ou coluna), a menos que envolvem a palavra em aspas (').
