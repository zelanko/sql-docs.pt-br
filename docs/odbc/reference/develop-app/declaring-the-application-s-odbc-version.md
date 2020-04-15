---
title: Declarando o Aplicativo&#39;versão ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba346ed7f7a261446110c5513026d20a86fd3a19
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285226"
---
# <a name="declaring-the-application39s-odbc-version"></a>Declarando o aplicativo&#39;versão ODBC
Antes de um aplicativo alocar uma conexão, ele deve definir o atributo do ambiente SQL_ATTR_ODBC_VERSION. Este atributo afirma que o aplicativo segue a especificação ODBC *2.x* ou ODBC *3.x* ao usar os seguintes itens:  
  
-   **SQLSTATES**. Muitos valores de SQLSTATE são diferentes em ODBC *2.x* e ODBC *3.x*.  
  
-   **Identificadores de tipo de data, hora e carimbo de tempo**. A tabela a seguir mostra os identificadores de tipo para dados de data, hora e carimbo de data no ODBC *2.x* e ODBC *3.x*.  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**Identificadores de tipo SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificadores de tipo C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _Argumento de nome_  **de catálogo em Tabelas SQL**. No ODBC *2.x,* os caracteres curinga ("%" e "_") no argumento *CatalogName* são tratados literalmente. No ODBC *3.x,* eles são tratados como caracteres curinga. Assim, um aplicativo que segue a especificação ODBC *2.x* não pode usá-los como caracteres curinga e não escapa a eles ao usá-los como literals. Um aplicativo que segue a especificação ODBC *3.x* pode usá-los como caracteres curinga ou escapar deles e usá-los como literals. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 Os driver manager oDBC *3.x* e os drivers ODBC *3.x* verificam a versão da especificação ODBC à qual um aplicativo é escrito e respondem de acordo. Por exemplo, se o aplicativo seguir a especificação ODBC *2.x* e chamar **SQLExecute** antes de chamar **o SQLPrepare,** o Gerenciador de Driver ODBC *3.x* retorna SQLSTATE S1010 (erro de seqüência de função). Se o aplicativo seguir a especificação ODBC *3.x,* o Driver Manager retorna SQLSTATE HY010 (erro de seqüência de funções). Para obter mais informações, consulte [Retrocompatibilidade e Conformidade de Padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Os aplicativos que seguem a especificação ODBC *3.x* devem usar código condicional para evitar usar a funcionalidade nova no ODBC *3.x* ao trabalhar com drivers ODBC *2.x.* Os drivers ODBC *2.x* não suportam funcionalidade nova para ODBC *3.x* apenas porque o aplicativo declara que segue a especificação ODBC *3.x.* Além disso, os drivers ODBC *3.x* não deixam de suportar funcionalidade nova no ODBC *3.x* apenas porque o aplicativo declara que segue a especificação ODBC *2.x.*
