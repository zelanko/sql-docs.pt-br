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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63313e3dfaec8dbcd91f3bb084bbaab46da40c6e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306777"
---
# <a name="using-concise-functions"></a>Usar funções concisas
Algumas funções ODBC ganham acesso implícito aos descritores. Os escritores de aplicativos podem encontrá-los mais convenientes do que ligar para **sqlsetdescField** ou **SQLGetDescField**. Essas funções são chamadas de funções *concisas* porque executam uma série de funções, incluindo a configuração ou obtenção de campos descritores. Algumas funções concisas permitem que um aplicativo defina ou recupere vários campos de descritores relacionados em uma única chamada de função.  
  
 Funções concisas podem ser chamadas sem antes recuperar uma alça descritor para uso como argumento. Essas funções funcionam com os campos descritores associados à alça de declaração em que são chamados.  
  
 As funções concisas **SQLBindCol** e **SQLBindParameter** ligam uma coluna ou parâmetro definindo os campos descritores que correspondem aos seus argumentos. Cada uma dessas funções executa mais tarefas do que simplesmente definir descritores. **SQLBindCol** e **SQLBindParameter** fornecem uma especificação completa da vinculação de uma coluna de dados ou parâmetro dinâmico. Um aplicativo pode, no entanto, alterar detalhes individuais de uma vinculação chamando **SQLSetDescField** ou **SQLSetDescRec** e pode vincular completamente uma coluna ou parâmetro fazendo uma série de chamadas adequadas para essas funções.  
  
 As funções concisas **SQLColAttribute,** **SQLDescribeCol,** **SQLDescribeParam,** **SQLNumParams**e **SQLNumResultCols** recuperam valores em campos descritores.  
  
 **SQLSetDescRec** e **SQLGetDescRec** são funções concisas que, com uma chamada, definem ou recebem vários campos de descritor que afetam o tipo de dados e o armazenamento de dados de coluna ou parâmetro. **SQLSetDescRec** é uma maneira eficaz de alterar a vinculação de dados de coluna ou parâmetro em uma etapa.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** servem como funções concisas em alguns casos. (Ver [Campos do Descritor](../../../odbc/reference/develop-app/descriptor-fields.md).)
