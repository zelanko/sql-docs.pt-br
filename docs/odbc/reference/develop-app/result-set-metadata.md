---
title: Metadados do conjunto de resultados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1aa59dd088611043a3212366f344ba0bae0cffc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="result-set-metadata"></a>Metadados de conjunto de resultados
*Metadados* são dados que descrevem outros dados. Por exemplo, os metadados do conjunto de resultados descrevem o conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados de colunas, seus nomes, precisão, nulidade e assim por diante.  
  
 Aplicativos interoperáveis sempre devem verificar os metadados das colunas do conjunto de resultados. Os metadados para uma coluna em um conjunto de resultados podem diferir dos metadados da coluna conforme retornado por uma função de catálogo. Por exemplo, suponha que uma coluna atualizável está incluída em um conjunto de resultados criado pela União de duas tabelas. Enquanto **SQLColumnPrivileges** pode indicar que um usuário pode atualizar a coluna, os metadados do conjunto de resultados podem não se a coluna é o lado "muitos" da associação; várias fontes de dados podem atualizar colunas no lado "um" de uma junção, mas não a " lado muitos". Até mesmo os tipos de dados não são considerados como iguais, porque a fonte de dados pode promover o tipo de dados ao criar o conjunto de resultados.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Como os metadados são usados?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
