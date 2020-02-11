---
title: Declarando a versão do ODBC do&#39;de aplicativos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea97e3cd7a8fee3b3397524bf2c48c428d6a0be0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076838"
---
# <a name="declaring-the-application39s-odbc-version"></a>Declarando a versão do aplicativo ODBC&#39;s
Antes que um aplicativo aloque uma conexão, ele deve definir o atributo de ambiente SQL_ATTR_ODBC_VERSION. Esse atributo declara que o aplicativo segue a especificação ODBC *2. x* ou ODBC *3. x* ao usar os seguintes itens:  
  
-   **SQLstates**. Muitos valores SQLSTATE são diferentes no ODBC *2. x* e no ODBC *3. x*.  
  
-   **Identificadores de tipo Date, time e timestamp**. A tabela a seguir mostra os identificadores de tipo para dados de data, hora e carimbo de hora no ODBC *2. x* e ODBC *3. x*.  
  
    |ODBC *2. x*|ODBC *3. x*|  
    |----------------|----------------|  
    |**Identificadores de tipo SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificadores de tipo C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   O argumento _CatalogName_**em SQLTables**.   No ODBC *2. x*, os caracteres curinga ("%" e "_") no argumento *CatalogName* são tratados literalmente. No ODBC *3. x*, eles são tratados como caracteres curinga. Assim, um aplicativo que segue a especificação ODBC *2. x* não pode usá-los como caracteres curinga e não os escapa ao usá-los como literais. Um aplicativo que segue a especificação ODBC *3. x* pode usá-los como caracteres curingas ou escape-los e usá-los como literais. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 Os drivers ODBC *3. x* Driver Manager e ODBC *3. x* verificam a versão da especificação ODBC para a qual um aplicativo é escrito e respondem de acordo. Por exemplo, se o aplicativo seguir a especificação ODBC *2. x* e chamar **SQLExecute** antes de chamar **SQLPrepare**, o Gerenciador de driver ODBC *3. x* retornará SQLSTATE S1010 (erro de sequência de função). Se o aplicativo seguir a especificação ODBC *3. x* , o Gerenciador de driver retornará SQLSTATE HY010 (erro de sequência de função). Para obter mais informações, consulte [compatibilidade com versões anteriores e conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Os aplicativos que seguem a especificação ODBC *3. x* devem usar o código condicional para evitar o uso da funcionalidade nova para ODBC *3. x* ao trabalhar com drivers ODBC *2. x* . Os drivers ODBC *2. x* não dão suporte à funcionalidade nova para o ODBC *3. x* apenas porque o aplicativo declara que segue a especificação do ODBC *3. x* . Além disso, os drivers ODBC *3. x* não deixam de oferecer suporte à funcionalidade nova para o ODBC *3. x* apenas porque o aplicativo declara que segue a especificação ODBC *2. x* .
