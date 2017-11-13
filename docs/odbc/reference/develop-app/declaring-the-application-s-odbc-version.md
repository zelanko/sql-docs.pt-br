---
title: "Declarando o aplicativo &#39; s ODBC versão | Microsoft Docs"
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
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32bfeff983ef5dff4ebfe3e575bcf36e855184d0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="declaring-the-application39s-odbc-version"></a>Declarando o aplicativo &#39; s versão do ODBC
Antes de um aplicativo aloca uma conexão, ele deve definir o atributo de ambiente SQL_ATTR_ODBC_VERSION. Esse atributo indica que o aplicativo segue o ODBC 2. *x* ou ODBC 3. *x* especificação ao usar os seguintes itens:  
  
-   **SQLSTATEs**. Muitos valores SQLSTATE são diferentes no ODBC 2. *x* e ODBC 3. *x*.  
  
-   **Data, hora e identificadores de tipo de carimbo de hora**. A tabela a seguir mostra os identificadores de tipo de data, hora e dados de carimbo de hora no ODBC 2. *x* e ODBC 3. *x*.  
  
    |ODBC 2. *x*|ODBC 3. *x*|  
    |----------------|----------------|  
    |**Identificadores de tipo SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificadores de tipo C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   *CatalogName***argumento SQLTables**.   No ODBC 2. *x*, os caracteres curinga ("%" e "_") no *CatalogName* argumento são tratados literalmente. Em ODBC 3. *x*, eles são tratados como caracteres curinga. Assim, um aplicativo que segue o ODBC 2. *x* especificação não é possível usá-los como escape-los não quando usá-los como literais e caracteres curinga. Um aplicativo que segue o ODBC 3. *x* especificação pode usá-los como caracteres curinga ou reservá-los e usá-los como literais. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 O ODBC 3*. x* Gerenciador de Driver e o ODBC 3*. x* drivers verificar a versão da especificação do ODBC para o qual um aplicativo é escrito e respondam adequadamente. Por exemplo, se o aplicativo segue o ODBC 2. *x* especificação e chamadas **SQLExecute** antes de chamar **SQLPrepare**, o ODBC 3*. x* Gerenciador de Driver retornará SQLSTATE S1010 ( Erro de sequência de função). Se o aplicativo segue o ODBC 3*. x* especificação, o Gerenciador de Driver retornará SQLSTATE HY010 (erro de sequência de função). Para obter mais informações, consulte [compatibilidade com versões anteriores e a conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Aplicativos que seguem o ODBC 3. *x* especificação deve usar o código condicional para evitar o uso de funcionalidade nova para ODBC 3. *x* ao trabalhar com ODBC 2. *x* drivers. ODBC 2. *x* drivers não oferecem suporte a funcionalidade nova para ODBC 3. *x* apenas porque o aplicativo declara que ele segue o ODBC 3. *x* especificação. Além disso, o ODBC 3. *x* drivers não dão suporte à funcionalidade nova para ODBC 3. *x* apenas porque o aplicativo declara que ele segue o ODBC 2. *x* especificação.

