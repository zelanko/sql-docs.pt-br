---
title: Usando funções concisas | Microsoft Docs
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
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c53a628eaaa3ca8348ce8917ace36da35c33f653
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915571"
---
# <a name="using-concise-functions"></a>Usando funções concisas
Algumas funções ODBC acessem implícita descritores. Autores de aplicativos podem encontrá-los mais convenientes do que chamar **SQLSetDescField** ou **SQLGetDescField**. Essas funções são chamadas *concisa* funções porque elas executam várias funções, incluindo a configuração ou obter campos de descritor. Algumas funções concisas permitem que um aplicativo definir ou recuperar vários campos de descritor relacionados em uma única chamada de função.  
  
 Funções concisas podem ser chamadas sem primeiro recuperar um indicador de descritor para uso como um argumento. Essas funções funcionam com os campos de descritor associados com o identificador de instrução que são chamadas.  
  
 As funções concisas **SQLBindCol** e **SQLBindParameter** associar uma coluna ou parâmetro definindo os campos de descritor que correspondem aos seus argumentos. Cada uma dessas funções executa tarefas mais do que simplesmente definindo descritores. **SQLBindCol** e **SQLBindParameter** fornecem uma especificação completa da associação de uma coluna de dados ou o parâmetro dinâmico. Um aplicativo pode, no entanto, alterar detalhes individuais de uma associação chamando **SQLSetDescField** ou **SQLSetDescRec** e completamente pode associar uma coluna ou parâmetro, fazendo uma série de chamadas adequadas para Essas funções.  
  
 As funções concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, e  **SQLNumResultCols** recuperar valores nos campos de descritor.  
  
 **SQLSetDescRec** e **SQLGetDescRec** concisa funções, com uma chamada, definir ou obter vários campos de descritor que afetam o tipo de dados e armazenamento de dados de coluna ou parâmetro. **SQLSetDescRec** é uma maneira eficiente para alterar a associação de dados de coluna ou parâmetro em uma única etapa.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** servem como funções concisas em alguns casos. (Consulte [campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md).)
