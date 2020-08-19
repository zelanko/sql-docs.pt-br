---
description: Metadados de conjunto de resultados
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46738682900509d22df1eebaa22b13d3abfb729e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424588"
---
# <a name="result-set-metadata"></a>Metadados de conjunto de resultados
*Metadados* são dados que descrevem outros dados. Por exemplo, os metadados do conjunto de resultados descrevem o conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados dessas colunas, seus nomes, precisão, nulidade e assim por diante.  
  
 Os aplicativos interoperáveis sempre devem verificar os metadados das colunas do conjunto de resultados. Os metadados de uma coluna em um conjunto de resultados podem ser diferentes dos metadados da coluna, conforme retornado por uma função de catálogo. Por exemplo, suponha que uma coluna atualizável seja incluída em um conjunto de resultados criado unindo-se duas tabelas. Embora **SQLColumnPrivileges** possa indicar que um usuário pode atualizar a coluna, os metadados do conjunto de resultados podem não se a coluna estiver no lado "muitos" da junção; muitas fontes de dados podem atualizar colunas no lado "um" de uma junção, mas não no lado "muitos". Até mesmo tipos de dados não podem ser considerados iguais, pois a fonte de dados pode promover o tipo de dados ao criar o conjunto de resultados.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Como os metadados são usados?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
