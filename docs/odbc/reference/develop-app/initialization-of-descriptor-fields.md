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
ms.openlocfilehash: c78162bcf0421fee609abe5fcacf9613e0f8020b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138935"
---
# <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor
Quando um descritor de linha de aplicativo é alocado, seus campos recebem valores iniciais conforme indicado em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). O valor inicial do campo SQL_DESC_TYPE é SQL_DEFAULT. Isso fornece um tratamento padrão de dados de banco de dados para apresentação para o aplicativo. O aplicativo pode especificar um tratamento diferente dos dados definindo os campos do registro do descritor.  
  
 O valor inicial de SQL_DESC_ARRAY_SIZE no cabeçalho do descritor é 1. O aplicativo pode modificar esse campo para habilitar a busca de LinhaMúltipla.  
  
 O conceito de valor padrão não é válido para os campos de um IRD. Um aplicativo pode obter acesso aos campos de um IRD somente quando há uma instrução preparada ou executada associada a ele.  
  
 Determinados campos de um IPD são definidos somente depois que o IPD é preenchido automaticamente pelo driver. Caso contrário, eles serão indefinidos. Esses campos são SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED e SQL_DESC_LOCAL_TYPE_NAME.
