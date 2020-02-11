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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022202"
---
# <a name="using-concise-functions"></a>Usar funções concisas
Algumas funções ODBC recebem acesso implícito aos descritores. Os gravadores de aplicativos podem encontrá-los mais convenientes do que chamar **SQLSetDescField** ou **SQLGetDescField**. Essas funções são chamadas de funções *concisas* porque executam várias funções, incluindo configuração ou obtenção de campos de descritor. Algumas funções concisas permitem que um aplicativo defina ou recupere vários campos de descritor relacionados em uma única chamada de função.  
  
 Funções concisas podem ser chamadas sem primeiro recuperar um identificador de descritor para uso como um argumento. Essas funções funcionam com os campos de descritor associados ao identificador de instrução em que eles são chamados.  
  
 As funções concisas **SQLBindCol** e **SQLBindParameter** associam uma coluna ou um parâmetro definindo os campos do descritor que correspondem aos seus argumentos. Cada uma dessas funções executa mais tarefas do que simplesmente definir descritores. **SQLBindCol** e **SQLBindParameter** fornecem uma especificação completa da Associação de uma coluna de dados ou parâmetro dinâmico. No entanto, um aplicativo pode alterar detalhes individuais de uma associação chamando **SQLSetDescField** ou **SQLSetDescRec** e pode associar completamente uma coluna ou um parâmetro, fazendo uma série de chamadas adequadas para essas funções.  
  
 As funções concisas **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**e **SQLNumResultCols** recuperam valores nos campos de descritor.  
  
 **SQLSetDescRec** e **SQLGetDescRec** são funções concisas que, com uma chamada, definem ou obtêm vários campos de descritor que afetam o tipo de dados e o armazenamento de dados de coluna ou parâmetro. **SQLSetDescRec** é uma maneira eficaz de alterar a associação de dados de coluna ou parâmetro em uma única etapa.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** servem como funções concisas em alguns casos. (Consulte os [campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md).)
