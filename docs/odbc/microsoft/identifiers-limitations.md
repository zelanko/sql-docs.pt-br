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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952395"
---
# <a name="identifiers-limitations"></a>Limitações de identificadores
Se um identificador contiver um espaço ou um símbolo especial, o identificador deverá ser colocado entre aspas. Um nome válido é uma cadeia de caracteres com até 64 caracteres, dos quais o primeiro caractere não deve ser um espaço. Os nomes válidos não podem incluir caracteres de controle ou os seguintes caracteres especiais: ' &#124; # *? [ ] . ! $ .  
  
 Não use as palavras reservadas listadas na gramática do SQL no Apêndice C da *referência do programador de ODBC* (ou a forma abreviada dessas palavras reservadas) como identificadores (ou seja, nomes de tabela ou coluna), a menos que você coloque a palavra entre aspas de trás (').
