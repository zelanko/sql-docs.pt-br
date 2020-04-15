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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286246"
---
# <a name="identifiers-limitations"></a>Limitações de identificadores
Se um identificador contiver um espaço ou um símbolo especial, o identificador deve ser incluído entre aspas traseiras. Um nome válido é uma seqüência de não mais de 64 caracteres, dos quais o primeiro caractere não deve ser um espaço. Nomes válidos não podem incluir caracteres de controle ou os seguintes caracteres especiais: ' &#124; # * ? [ ] . ! $ .  
  
 Não use as palavras reservadas listadas na gramática SQL no apêndice C da *Referência do Programador ODBC* (ou a forma abreviada dessas palavras reservadas) como identificadores (isto é, nomes de tabela ou coluna), a menos que você cerque a palavra entre aspas (').
