---
title: Limitações de identificadores | Microsoft Docs
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
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 251ae0e4e94cec903e2c4b5cf687ed9b8b41dfc8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952395"
---
# <a name="identifiers-limitations"></a>Limitações de identificadores
Se um identificador contiver um espaço ou um símbolo especial, o identificador deve ser colocado entre aspas back. Um nome válido é uma cadeia de caracteres de não mais do que 64 caracteres, dos quais o primeiro caractere não deve ser um espaço. Nomes válidos não podem incluir caracteres de controle ou os seguintes caracteres especiais: ' &#124; # *? [ ] . ! $ .  
  
 Não use palavras reservadas listadas na gramática do SQL no Apêndice C do *referência do programador de ODBC* (ou a forma abreviada dessas palavras reservadas) como identificadores (ou seja, nomes tabela ou coluna), a menos que você coloque a palavra novamente aspas (').
