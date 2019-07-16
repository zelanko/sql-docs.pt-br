---
title: Metadados de conjunto de resultado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d8da8c15c861fff4767aa598e1b989d8f699c95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020594"
---
# <a name="result-set-metadata"></a>Metadados de conjunto de resultados
*Metadados* são dados que descrevem outros dados. Por exemplo, os metadados de conjunto de resultados descrevem o conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados dessas colunas, seus nomes, precisão, nulidade e assim por diante.  
  
 Aplicativos interoperáveis sempre devem verificar os metadados das colunas do conjunto de resultados. Os metadados para uma coluna em um conjunto de resultados podem diferir dos metadados da coluna conforme retornado por uma função de catálogo. Por exemplo, suponha que uma coluna atualizável está incluída em um conjunto de resultados criado unindo duas tabelas. Embora **SQLColumnPrivileges** pode indicar que um usuário pode atualizar a coluna, os metadados do conjunto de resultados podem não se a coluna for no lado "muitos" da união; muitas fontes de dados podem atualizar colunas no lado "um" de uma junção, mas não a " lado muitos". Até mesmo os tipos de dados não são considerados ser o mesmo, porque a fonte de dados pode promover o tipo de dados ao criar o conjunto de resultados.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Como os metadados são usados?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
