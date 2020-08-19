---
description: Campos adiados
title: Campos adiados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8b313f2d77270e95830de1a524706aa7fe36e33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424688"
---
# <a name="deferred-fields"></a>Campos adiados
Os valores dos *campos adiados* não são usados quando eles são definidos, mas o driver salva os endereços das variáveis para um efeito adiado. Para um descritor de parâmetro de aplicativo, o driver usa o conteúdo das variáveis no momento da chamada para **SQLExecDirect** ou **SQLExecute**. Para um descritor de linha de aplicativo, o driver usa o conteúdo das variáveis no momento da busca.  
  
 Os seguintes são os campos adiados:  
  
-   Os campos SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR de um registro de descritor.  
  
-   O campo SQL_DESC_OCTET_LENGTH_PTR de um registro de descritor de aplicativo.  
  
-   No caso de uma busca de LinhaMúltipla, os campos SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR de um cabeçalho de descritor.  
  
 Quando um descritor é alocado, os campos adiados de cada registro de descritor inicialmente têm um valor nulo. O significado do valor nulo é o seguinte:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR tiver um valor nulo, uma busca de LinhaMúltipla falhará ao retornar esse componente das informações de diagnóstico por linha.  
  
-   Se SQL_DESC_DATA_PTR tiver um valor nulo, o registro será não associado.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um ARD tiver um valor nulo, o driver não retornará informações de comprimento para essa coluna.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um APD tiver um valor nulo e o parâmetro for uma cadeia de caracteres, o driver assumirá que a cadeia de caracteres é terminada em nulo. Para parâmetros dinâmicos de saída, um valor nulo nesse campo impede que o driver retorne informações de comprimento. (Se o campo SQL_DESC_TYPE não indicar um parâmetro de cadeia de caracteres, o campo SQL_DESC_OCTET_LENGTH_PTR será ignorado.)  
  
 O aplicativo não deve desalocar ou descartar variáveis usadas para campos adiados entre o tempo que as associa aos campos e a hora em que o driver lê ou grava.
