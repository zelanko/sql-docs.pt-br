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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9aca006623d9ddb8292147d8a28c93f912fd25d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794019"
---
# <a name="bookmark-types"></a>Tipos de indicador
Todos os indicadores no ODBC *3.x* são indicadores de comprimento variável. Isso permite que uma chave primária ou um índice exclusivo associado a uma tabela a ser usado como um indicador. O indicador também pode ser um valor de 32 bits, que foi usada no ODBC *2.x*. Para especificar que um indicador é usado com um cursor, e um ODBC *3.x* aplicativo define o atributo da instrução SQL_ATTR_USE_BOOKMARK como SQL_UB_VARIABLE. Um indicador de comprimento variável será usado automaticamente.  
  
 Um aplicativo pode chamar **SQLColAttribute** com o *FieldIdentifier* argumento definido como SQL_DESC_OCTET_LENGTH para obter o comprimento do indicador. Como um indicador de comprimento variável pode ser um valor longo, um aplicativo não deve associar a coluna 0, a menos que ele usará o indicador para muitas das linhas no conjunto de linhas.  
  
 Indicadores de comprimento fixo têm suporte somente para compatibilidade com versões anteriores. Se um ODBC *2.x* aplicativo trabalhar com ODBC *3.x* driver chama **SQLSetStmtOption** para definir SQL_USE_BOOKMARKS SQL_UB_ON, ele é mapeado no Gerenciador de Driver para SQL _ UB_VARIABLE. Um indicador de comprimento variável será usado, mesmo se apenas de 32 bits dele são preenchidos. Se um driver dá suporte a indicadores de comprimento fixo, ele oferecerá suporte a indicadores de comprimento variável. Se um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE, ele é mapeado no Driver Gerenciador de SQL_UB_ON e um indicador de comprimento fixo de 32 bits é usado. O atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR, em seguida, deve apontar para um indicador de 32 bits. Se os indicadores usados são mais de 32 bits, como quando as chaves primárias são usadas como indicadores, o cursor deve mapear os valores reais para valores de 32 bits. Ele poderia, por exemplo, crie uma tabela de hash deles. Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver é associado a um indicador, o comprimento do buffer deve ser 4.
