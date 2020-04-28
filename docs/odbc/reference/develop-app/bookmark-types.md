---
title: Tipos de indicador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d0297cd9dc57e9f30945a9248b235ae469da3e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306327"
---
# <a name="bookmark-types"></a>Tipos de indicador
Todos os indicadores no ODBC *3. x* são indicadores de comprimento variável. Isso permite que uma chave primária ou um índice exclusivo associado a uma tabela seja usado como um indicador. O indicador também pode ser um valor de 32 bits, como foi usado no ODBC *2. x*. Para especificar que um indicador é usado com um cursor, um aplicativo ODBC *3. x* define o atributo da instrução SQL_ATTR_USE_BOOKMARK como SQL_UB_VARIABLE. Um indicador de comprimento variável é usado automaticamente.  
  
 Um aplicativo pode chamar **SQLColAttribute** com o argumento *FieldIdentifier* definido como SQL_DESC_OCTET_LENGTH para obter o comprimento do indicador. Como um indicador de comprimento variável pode ser um valor longo, um aplicativo não deve se associar à coluna 0, a menos que use o indicador para muitas das linhas no conjunto de linhas.  
  
 Há suporte para indicadores de comprimento fixo apenas para compatibilidade com versões anteriores. Se um aplicativo ODBC *2. x* que trabalha com um driver ODBC *3. x* chamar **SQLSetStmtOption** para definir SQL_USE_BOOKMARKS como SQL_UB_ON, ele será mapeado no Gerenciador de driver para SQL_UB_VARIABLE. Um indicador de comprimento variável é usado, mesmo que apenas 32 bits de ti sejam preenchidos. Se um driver oferecer suporte a indicadores de comprimento fixo, ele dará suporte a indicadores de comprimento variável. Se um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chamar **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE, ele será mapeado no Gerenciador de driver para SQL_UB_ON e um indicador de comprimento fixo de 32 bits será usado. O atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR deve apontar para um indicador de 32 bits. Se os indicadores usados tiverem mais de 32 bits, como quando as chaves primárias forem usadas como indicadores, o cursor deverá mapear os valores reais para valores de 32 bits. Ele pode, por exemplo, criar uma tabela de hash deles. Quando um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* associa um indicador, o comprimento do buffer deve ser 4.
