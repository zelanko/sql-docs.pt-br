---
title: Metadados de conjunto de resultados | Microsoft Docs
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
ms.openlocfilehash: 3b78cdeb4c8b3522f4677c0277401cd9395a36a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300076"
---
# <a name="result-set-metadata"></a>Metadados de conjunto de resultados
*Metadados* são dados que descrevem outros dados. Por exemplo, metadados de conjunto de resultados descrevem o conjunto de resultados, como o número de colunas no conjunto de resultados, os tipos de dados dessas colunas, seus nomes, precisão, nulidade e assim por diante.  
  
 Os aplicativos interoperáveis devem sempre verificar os metadados das colunas de conjunto de resultados. Os metadados de uma coluna em um conjunto de resultados podem diferir dos metadados para a coluna como retornados por uma função de catálogo. Por exemplo, suponha que uma coluna updatable seja incluída em um conjunto de resultados criado pela junção de duas tabelas. Embora **o SQLColumnPrivileges** possa indicar que um usuário pode atualizar a coluna, os metadados definidos em resultado podem não se a coluna estiver no lado "muitos" da parte; muitas fontes de dados podem atualizar colunas no lado "um" de uma junta, mas não no lado "muitos". Mesmo os tipos de dados não podem ser considerados os mesmos, porque a fonte de dados pode promover o tipo de dados ao criar o conjunto de resultados.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Como os metadados são usados?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
