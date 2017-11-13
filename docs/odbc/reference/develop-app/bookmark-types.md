---
title: Tipos de indicadores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a4ab42d7a8b18ebb2b37c871f46981c69c84b908
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="bookmark-types"></a>Tipos de indicador
Todos os indicadores em ODBC 3*. x* são indicadores de comprimento variável. Isso permite que uma chave primária ou um índice exclusivo associado a uma tabela a ser usado como um indicador. O indicador também pode ser um valor de 32 bits, que foi usada no ODBC 2. *x*. Para especificar que um indicador é usado com um cursor, um ODBC 3*. x* aplicativo define o atributo de instrução SQL_ATTR_USE_BOOKMARK para SQL_UB_VARIABLE. Um indicador de comprimento variável será usado automaticamente.  
  
 Um aplicativo pode chamar **SQLColAttribute** com o *FieldIdentifier* argumento definido como SQL_DESC_OCTET_LENGTH para obter o comprimento do indicador. Como um indicador de comprimento variável pode ser um valor longo, um aplicativo não deve associar a coluna 0, a menos que ele usará o indicador para muitas das linhas no conjunto de linhas.  
  
 Indicadores de comprimento fixo têm suporte somente para compatibilidade com versões anteriores. Se um ODBC 2. *x* aplicativo trabalhando com um ODBC 3*. x* driver chama **SQLSetStmtOption** para definir SQL_USE_BOOKMARKS para SQL_UB_ON, ele é mapeado para SQL_UB_VARIABLE no Gerenciador de Driver . Um indicador de comprimento variável será usado, mesmo se somente 32 bits dele são preenchidos. Se um driver dá suporte a indicadores de comprimento fixo, ela dará suporte a indicadores de comprimento variável. Se um ODBC 3*. x* aplicativo trabalhando com um ODBC 2. *x* driver chama **SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE, ele é mapeado para SQL_UB_ON no Gerenciador de Driver e um indicador de comprimento fixo de 32 bits é usado. O atributo da instrução SQL_ATTR_FETCH_BOOKMARK_PTR, em seguida, deve apontar para um indicador de 32 bits. Se os marcadores usados são mais de 32 bits, como quando as chaves primárias são usadas como indicadores, o cursor deve mapear os valores reais para valores de 32 bits. Ele pode, por exemplo, criar uma tabela de hash deles. Quando um ODBC 3*. x* aplicativo trabalhando com um ODBC 2. *x* driver associa um indicador, o tamanho do buffer deve ser 4.

