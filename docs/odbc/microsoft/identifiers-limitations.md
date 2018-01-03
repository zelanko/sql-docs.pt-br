---
title: "Limitações de identificadores | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc9deecbd06b3bcb0aec9d3e0d3b8790c7af0b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="identifiers-limitations"></a>Limitações de identificadores
Se um identificador contiver um espaço ou um símbolo especial, o identificador deve ser colocado entre aspas voltar. Um nome válido é uma cadeia de caracteres de não mais do que 64 caracteres, dos quais o primeiro caractere não deve ser um espaço. Os nomes válidos não podem incluir caracteres de controle ou os seguintes caracteres especiais: ' &#124; # * ? [ ] . ! $ .  
  
 Não use palavras reservadas listadas na gramática SQL no Apêndice C do *referência do programador de ODBC* (ou a forma abreviada dessas palavras reservadas) como identificadores (ou seja, nomes tabela ou coluna), a menos que envolvem a palavra em aspas (').
