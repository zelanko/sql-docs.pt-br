---
title: Adiado campos | Microsoft Docs
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
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc2020dc36ce031391194695e40308431c0f06d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910261"
---
# <a name="deferred-fields"></a>Campos adiados
Os valores de *adiada campos* não são usadas quando eles são definidos, mas o driver salva os endereços das variáveis para um efeito adiada. Para um descritor de parâmetro de aplicativo, o driver usa o conteúdo das variáveis no momento da chamada para **SQLExecDirect** ou **SQLExecute**. Para um descritor de linha de aplicativo, o driver usa o conteúdo das variáveis no momento da busca.  
  
 A seguir estão campos adiados:  
  
-   Os campos de um registro do descritor SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR.  
  
-   O campo SQL_DESC_OCTET_LENGTH_PTR de um registro do descritor de aplicativo.  
  
-   No caso de uma busca de várias linhas, os campos SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR de um cabeçalho do descritor.  
  
 Quando um descritor é alocado, campos adiados de cada registro do descritor inicialmente tem um valor nulo. O significado do valor nulo é da seguinte maneira:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR tem um valor nulo, uma busca multilinha Falha ao retornar este componente das informações de diagnóstico por linha.  
  
-   Se SQL_DESC_DATA_PTR tem um valor nulo, o registro é desassociado.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um descartar tem um valor nulo, o driver não retorna informações de comprimento de coluna.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um APD tem um valor nulo e o parâmetro é uma cadeia de caracteres, o driver pressupõe que a cadeia de caracteres é terminada em nulo. Parâmetros de saída dinâmica, um valor nulo no campo impede que o driver retornando informações de comprimento. (Se o campo SQL_DESC_TYPE não indicar um parâmetro de cadeia de caracteres, o campo SQL_DESC_OCTET_LENGTH_PTR é ignorado.)  
  
 O aplicativo não deve ser desalocada ou descarte variáveis usadas para campos adiados entre a hora em que associa-os com os campos e a hora em que o driver lê ou grava.
