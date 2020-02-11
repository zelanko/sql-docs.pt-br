---
title: Metadados do conjunto de resultados | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020594"
---
# <a name="result-set-metadata"></a>Metadados de conjunto de resultados
*Metadados* são dados que descrevem outros dados. Por exemplo, os metadados do conjunto de resultados descrevem o conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados dessas colunas, seus nomes, precisão, nulidade e assim por diante.  
  
 Os aplicativos interoperáveis sempre devem verificar os metadados das colunas do conjunto de resultados. Os metadados de uma coluna em um conjunto de resultados podem ser diferentes dos metadados da coluna, conforme retornado por uma função de catálogo. Por exemplo, suponha que uma coluna atualizável seja incluída em um conjunto de resultados criado unindo-se duas tabelas. Embora **SQLColumnPrivileges** possa indicar que um usuário pode atualizar a coluna, os metadados do conjunto de resultados podem não se a coluna estiver no lado "muitos" da junção; muitas fontes de dados podem atualizar colunas no lado "um" de uma junção, mas não no lado "muitos". Até mesmo tipos de dados não podem ser considerados iguais, pois a fonte de dados pode promover o tipo de dados ao criar o conjunto de resultados.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Como os metadados são usados?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
