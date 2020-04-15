---
title: Campos Diferidos | Microsoft Docs
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
ms.openlocfilehash: 094aba353e10ed568e1959b1d655109296507dee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305967"
---
# <a name="deferred-fields"></a>Campos adiados
Os valores dos *campos diferidos* não são usados quando são definidos, mas o driver salva os endereços das variáveis para um efeito diferido. Para um descritor de parâmetro de aplicativo, o driver usa o conteúdo das variáveis no momento da chamada para **SQLExecDirect** ou **SQLExecute**. Para um descritor de linha de aplicativo, o driver usa o conteúdo das variáveis no momento da busca.  
  
 Os seguintes campos são diferidos:  
  
-   O SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR campos de um registro descritor.  
  
-   O SQL_DESC_OCTET_LENGTH_PTR campo de um registro de descritor de aplicação.  
  
-   No caso de uma busca multirow, o SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR campos de um cabeçalho descritor.  
  
 Quando um descritor é alocado, os campos diferidos de cada registro descritor inicialmente têm um valor nulo. O significado do valor nulo é o seguinte:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR tiver um valor nulo, uma busca multirow não retorna este componente das informações de diagnóstico por linha.  
  
-   Se SQL_DESC_DATA_PTR tiver um valor nulo, o registro será desvinculado.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um ARD tiver um valor nulo, o driver não retornará as informações de comprimento para essa coluna.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de uma APD tiver um valor nulo e o parâmetro for uma seqüência de caracteres, o driver assumirá que a seqüência é anulada. Para parâmetros dinâmicos de saída, um valor nulo neste campo impede que o driver retorne as informações de comprimento. (Se o campo SQL_DESC_TYPE não indicar um parâmetro de seqüência de caracteres, o campo SQL_DESC_OCTET_LENGTH_PTR será ignorado.)  
  
 O aplicativo não deve desalocar ou descartar variáveis usadas para campos diferidos entre o momento em que os associa aos campos e o tempo em que o motorista lê ou escreve.
