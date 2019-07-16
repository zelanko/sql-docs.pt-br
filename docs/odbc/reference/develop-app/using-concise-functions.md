---
title: Usando funções concisas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43004601845d3032d404c308b7b1fa4850f694ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022202"
---
# <a name="using-concise-functions"></a>Usar funções concisas
Algumas funções ODBC acessem implícita descritores. Criadores de aplicativo podem encontrá-los mais convenientes do que chamar **SQLSetDescField** ou **SQLGetDescField**. Essas funções são chamadas *concisa* funções porque elas executam várias funções, incluindo a configuração ou obter campos de descritor. Algumas funções concisas permitem que um aplicativo definir ou recuperar vários campos de descritor relacionados em uma única chamada de função.  
  
 Funções concisas podem ser chamadas sem primeiro recuperar um identificador do descritor para uso como um argumento. Essas funções funcionam com os campos de descritor associados com o identificador de instrução que são chamadas.  
  
 As funções concisas **SQLBindCol** e **SQLBindParameter** associar uma coluna ou parâmetro definindo os campos de descritor que correspondem aos seus argumentos. Cada uma dessas funções executa mais tarefas do que simplesmente definindo descritores. **SQLBindCol** e **SQLBindParameter** fornecem uma especificação completa da associação de uma coluna de dados ou o parâmetro dinâmico. Um aplicativo pode, no entanto, alterar os detalhes individuais de uma associação chamando **SQLSetDescField** ou **SQLSetDescRec** e completamente pode associar uma coluna ou parâmetro, fazendo uma série de chamadas adequadas para Essas funções.  
  
 As funções concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, e  **SQLNumResultCols** recuperar os valores nos campos de descritor.  
  
 **SQLSetDescRec** e **SQLGetDescRec** são funções concisas que, com uma chamada, definir ou obtém vários campos de descritor que afetam o tipo de dados e armazenamento de dados de coluna ou parâmetro. **SQLSetDescRec** é uma maneira eficiente para alterar a associação de dados de coluna ou parâmetro em uma única etapa.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** servem como funções concisas em alguns casos. (Consulte [campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md).)
