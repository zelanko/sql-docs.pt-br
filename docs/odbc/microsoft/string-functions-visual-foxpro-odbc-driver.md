---
title: Funções de corda (driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 988ba23b95f6b138148b1fa17ad303d7aa2dc895
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299186"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>Funções de cadeia de caracteres (Driver ODBC do Visual FoxPro)
A tabela a seguir lista funções de manipulação de strings ODBC suportadas pelo Visual FoxPro ODBC Driver; quando a gramática Visual FoxPro para a mesma função difere da sintaxe ODBC, o equivalente Visual FoxPro é listado.  
  
|Gramática ODBC|Gramática Visual FoxPro|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(código)*|*CSC (string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|DIFERENÇA *(string_exp1, string_exp2)*||  
|INSERIR *(string_exp1, partida, comprimento, string_exp2)*|MATERIAL *(string_exp1, início, comprimento, string_exp2)*|  
|LCASE *(string_exp)*|INFERIOR *(string_exp)*|  
|ESQUERDA *(string_exp, contagem)*||  
|COMPRIMENTO *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPEAT *(string_exp, contagem)*|REPLICAR *(string_exp, contagem)*|  
|SUBSTITUA *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|DIREITA *(string_exp, contagem)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|ESPAÇO *(contagem)*||  
|SUBSTRING *(string_exp, início, comprimento)*|SUBSTR *(string_exp, início, comprimento)*|  
|UCASE *(string_exp)*|SUPERIOR *(string_exp)*|
