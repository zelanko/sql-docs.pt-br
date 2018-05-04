---
title: Inicialização de campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1875f69e3ba26a331b5042ebcdaaa803559f772a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor
Quando é alocado um descritor de linha de aplicativo, seus campos recebem valores iniciais, conforme indicado na [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). O valor inicial do campo SQL_DESC_TYPE é SQL_DEFAULT. Isso fornece um tratamento padrão de banco de dados para apresentação para o aplicativo. O aplicativo pode especificar tratamento diferente dos dados, definindo campos de registro do descritor.  
  
 O valor inicial da SQL_DESC_ARRAY_SIZE no cabeçalho do descritor é 1. O aplicativo pode modificar esse campo para habilitar busca multilinha.  
  
 O conceito de um valor padrão não é válido para os campos de um IRD. Um aplicativo pode obter acesso aos campos de um IRD somente quando há uma instrução preparada ou executada associada a ele.  
  
 Alguns campos de um IPD são definidos somente depois que o IPD foi preenchida automaticamente pelo driver. Se não, eles serão indefinidos. Esses campos são SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED e SQL_DESC_LOCAL_TYPE_NAME.
