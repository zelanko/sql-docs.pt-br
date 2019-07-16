---
title: Adiado campos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2c229d31941d5cef0da253545cecd7d1496ee4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076822"
---
# <a name="deferred-fields"></a>Campos adiados
Os valores de *adiada campos* não são usados quando elas estiverem definidas, mas o driver salva os endereços das variáveis para um efeito adiada. Para um descritor de parâmetro de aplicativo, o driver usa o conteúdo das variáveis no momento da chamada para **SQLExecDirect** ou **SQLExecute**. Para um descritor de linha de aplicativo, o driver usa o conteúdo das variáveis no momento da busca.  
  
 Estes são campos adiados:  
  
-   Os campos de um registro de descritor SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR.  
  
-   O campo SQL_DESC_OCTET_LENGTH_PTR de um registro de descritor de aplicativo.  
  
-   No caso de uma busca de várias linhas, os campos SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR de um cabeçalho do descritor.  
  
 Quando um descritor é alocado, campos adiados de cada registro de descritor inicialmente tem um valor nulo. O significado do valor nulo é da seguinte maneira:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR tem um valor nulo, uma busca de várias linhas não retornar esse componente das informações de diagnóstico por linha.  
  
-   Se SQL_DESC_DATA_PTR tem um valor nulo, o registro é não associado.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um descartar tem um valor nulo, o driver não retorna informações de comprimento para aquela coluna.  
  
-   Se o campo SQL_DESC_OCTET_LENGTH_PTR de um APD tem um valor nulo e o parâmetro é uma cadeia de caracteres, o driver pressupõe que a cadeia de caracteres é terminada em nulo. Dinâmicos para parâmetros de saída, um valor nulo nesse campo impede que o driver retornando informações de comprimento. (Se o campo SQL_DESC_TYPE não indicar um parâmetro de cadeia de caracteres, o campo SQL_DESC_OCTET_LENGTH_PTR é ignorado.)  
  
 O aplicativo não deve desalocar ou descartar as variáveis usadas para os campos adiados entre a hora em que ele associa-os com os campos e a hora em que o driver lê ou grava-os.
