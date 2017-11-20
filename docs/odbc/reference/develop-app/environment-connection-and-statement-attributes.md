---
title: "Atributos de instrução, Conexão e ambiente | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dfe477bf0ca518d4f4e83d141a24bcb4c2640ed2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="environment-connection-and-statement-attributes"></a>Ambiente, Conexão e atributos de instrução
ODBC define um número de atributos que estão associados a ambientes, conexões ou instruções.  
  
 Atributos de ambiente afetam todo o ambiente, como se o pool de conexão está habilitado. Atributos de ambiente são definidos com **SQLSetEnvAttr** e recuperados com **SQLGetEnvAttr**.  
  
 Atributos de Conexão afetam cada conexão individualmente, por exemplo, como tempo um driver deve aguardar ao tentar se conectar a uma fonte de dados antes do tempo limite. Atributos de Conexão são definidos com **SQLSetConnectAttr** e recuperados com **SQLGetConnectAttr**. Para obter mais informações sobre atributos de conexão, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Atributos de instrução afetam cada instrução individualmente, como se uma instrução deve ser executada de forma assíncrona. Atributos de instrução são definidos com **SQLSetStmtAttr** e recuperados com **SQLGetStmtAttr**. Alguns atributos de instrução são os atributos somente leitura e não podem ser definidos. Por exemplo, o atributo de instrução SQL_ATTR_ROW_NUMBER, que é usado para recuperar o número da linha atual do cursor, é somente leitura. Para obter mais informações sobre atributos de instrução, consulte [atributos de instrução](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Além dos atributos definidos por ODBC, um driver pode definir sua própria conexão e os atributos de instrução. Atributos definidos pelo driver devem ser registrados com o Open Group para garantir que dois fornecedores de driver não atribua o mesmo valor de inteiro para atributos diferentes, proprietários. Para obter mais informações, consulte [tipos de dados específicos do Driver, tipos de descritor, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obter uma lista completa de atributos, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). A maioria dos atributos também são descritos na descrição da função de ODBC que elas afetam.

