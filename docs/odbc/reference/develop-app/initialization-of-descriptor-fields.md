---
title: Inicialização de Campos Descritores | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300116"
---
# <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor
Quando um descritor de linha de aplicativo é alocado, seus campos recebem valores iniciais conforme indicado no [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). O valor inicial do campo SQL_DESC_TYPE é SQL_DEFAULT. Isso prevê um tratamento padrão dos dados do banco de dados para apresentação ao aplicativo. O aplicativo pode especificar diferentes tratamentos dos dados definindo campos do registro do descritor.  
  
 O valor inicial de SQL_DESC_ARRAY_SIZE no cabeçalho do descritor é 1. O aplicativo pode modificar este campo para permitir a busca multirow.  
  
 O conceito de um valor padrão não é válido para os campos de um IRD. Um aplicativo pode ter acesso aos campos de um IRD somente quando houver uma declaração preparada ou executada associada a ele.  
  
 Certos campos de um IPD são definidos somente após o IPD ter sido preenchido automaticamente pelo driver. Se não, eles são indefinidos. Esses campos são SQL_DESC_CASE_SENSITIVE, SQL_DESC_FIXED_PREC_SCALE, SQL_DESC_TYPE_NAME, SQL_DESC_UNSIGNED e SQL_DESC_LOCAL_TYPE_NAME.
