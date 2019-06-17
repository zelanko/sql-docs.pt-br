---
title: Inicialização de campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d988099cad357254f04a79a8a6cccbbe4eb2768c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446807"
---
# <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor
Quando um descritor de linha de aplicativo é alocado, seus campos recebem valores iniciais, conforme indicado na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). O valor inicial do campo SQL_DESC_TYPE é SQL_DEFAULT. Isso fornece um tratamento padrão de banco de dados para apresentação para o aplicativo. O aplicativo pode especificar tratamento diferente dos dados, definindo os campos do registro do descritor.  
  
 O valor inicial de SQL_DESC_ARRAY_SIZE no cabeçalho do descritor é 1. O aplicativo pode modificar esse campo para habilitar a busca de várias linhas.  
  
 O conceito de um valor padrão não é válido para os campos de um IRD. Um aplicativo pode obter acesso aos campos de um IRD somente quando há uma instrução preparada ou executada associada a ele.  
  
 Determinados campos de um IPD são definidos somente depois que o IPD foi preenchida automaticamente pelo driver. Se não estiver, eles são indefinidos. Esses campos são SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED e SQL_DESC_LOCAL_TYPE_NAME.
