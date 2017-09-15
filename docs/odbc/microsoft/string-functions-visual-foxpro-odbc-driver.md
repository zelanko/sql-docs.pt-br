---
title: "Cadeia de caracteres funções (Driver ODBC do Visual FoxPro) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3fa7491ea354cc616d6b58de17e6fa82c785a3a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>Funções de cadeia de caracteres (Driver ODBC do Visual FoxPro)
A tabela a seguir lista funções de manipulação de cadeia de caracteres ODBC com suporte do Visual FoxPro ODBC Driver; Quando a gramática do Visual FoxPro para a mesma função difere da sintaxe de ODBC, o Visual FoxPro equivalente é listado.  
  
|Gramática ODBC|Gramática do Visual FoxPro|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(código)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|DIFERENÇA *(string_exp1, string_exp2)*||  
|Inserir *(string_exp1, início, comprimento, string_exp2)*|COISAS *(string_exp1, início, comprimento, string_exp2)*|  
|LCASE *(string_exp)*|INFERIOR *(string_exp)*|  
|ESQUERDA *(string_exp, contagem)*||  
|COMPRIMENTO *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPITA *(string_exp, contagem)*|REPLICAR *(string_exp, contagem)*|  
|SUBSTITUIR *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|DIREITA *(string_exp, contagem)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|ESPAÇO *(contagem)*||  
|Subcadeia de caracteres *(string_exp, início, comprimento)*|SUBSTR *(string_exp, início, comprimento)*|  
|UCASE *(string_exp)*|SUPERIOR *(string_exp)*|
