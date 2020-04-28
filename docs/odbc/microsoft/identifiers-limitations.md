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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286246"
---
# <a name="identifiers-limitations"></a>Limitações de identificadores
Se um identificador contiver um espaço ou um símbolo especial, o identificador deverá ser colocado entre aspas. Um nome válido é uma cadeia de caracteres com até 64 caracteres, dos quais o primeiro caractere não deve ser um espaço. Os nomes válidos não podem incluir caracteres de controle ou os seguintes caracteres especiais: ' &#124; # *? [ ] . ! $ .  
  
 Não use as palavras reservadas listadas na gramática do SQL no Apêndice C da *referência do programador de ODBC* (ou a forma abreviada dessas palavras reservadas) como identificadores (ou seja, nomes de tabela ou coluna), a menos que você coloque a palavra entre aspas de trás (').
