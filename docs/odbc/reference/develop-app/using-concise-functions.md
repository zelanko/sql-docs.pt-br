---
title: "Usando funções concisas | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f58efc6ca7f6587ce7d7070bc02ad935efe06bff
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="using-concise-functions"></a>Usando funções concisas
Algumas funções ODBC acessem implícita descritores. Autores de aplicativos podem encontrá-los mais convenientes do que chamar **SQLSetDescField** ou **SQLGetDescField**. Essas funções são chamadas *concisa* funções porque elas executam várias funções, incluindo a configuração ou obter campos de descritor. Algumas funções concisas permitem que um aplicativo definir ou recuperar vários campos de descritor relacionados em uma única chamada de função.  
  
 Funções concisas podem ser chamadas sem primeiro recuperar um indicador de descritor para uso como um argumento. Essas funções funcionam com os campos de descritor associados com o identificador de instrução que são chamadas.  
  
 As funções concisas **SQLBindCol** e **SQLBindParameter** associar uma coluna ou parâmetro definindo os campos de descritor que correspondem aos seus argumentos. Cada uma dessas funções executa tarefas mais do que simplesmente definindo descritores. **SQLBindCol** e **SQLBindParameter** fornecem uma especificação completa da associação de uma coluna de dados ou o parâmetro dinâmico. Um aplicativo pode, no entanto, alterar detalhes individuais de uma associação chamando **SQLSetDescField** ou **SQLSetDescRec** e completamente pode associar uma coluna ou parâmetro, fazendo uma série de chamadas adequadas para Essas funções.  
  
 As funções concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, e  **SQLNumResultCols** recuperar valores nos campos de descritor.  
  
 **SQLSetDescRec** e **SQLGetDescRec** concisa funções, com uma chamada, definir ou obter vários campos de descritor que afetam o tipo de dados e armazenamento de dados de coluna ou parâmetro. **SQLSetDescRec** é uma maneira eficiente para alterar a associação de dados de coluna ou parâmetro em uma única etapa.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** servem como funções concisas em alguns casos. (Consulte [campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md).)
