---
title: Metadados do conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d309136c3682a781d4eef82e69e2a2f98a20efe2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911701"
---
# <a name="result-set-metadata"></a>Metadados de conjunto de resultados
*Metadados* são dados que descrevem outros dados. Por exemplo, os metadados do conjunto de resultados descrevem o conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados de colunas, seus nomes, precisão, nulidade e assim por diante.  
  
 Aplicativos interoperáveis sempre devem verificar os metadados das colunas do conjunto de resultados. Os metadados para uma coluna em um conjunto de resultados podem diferir dos metadados da coluna conforme retornado por uma função de catálogo. Por exemplo, suponha que uma coluna atualizável está incluída em um conjunto de resultados criado pela União de duas tabelas. Enquanto **SQLColumnPrivileges** pode indicar que um usuário pode atualizar a coluna, os metadados do conjunto de resultados podem não se a coluna é o lado "muitos" da associação; várias fontes de dados podem atualizar colunas no lado "um" de uma junção, mas não a " lado muitos". Até mesmo os tipos de dados não são considerados como iguais, porque a fonte de dados pode promover o tipo de dados ao criar o conjunto de resultados.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Como os metadados são usados?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
