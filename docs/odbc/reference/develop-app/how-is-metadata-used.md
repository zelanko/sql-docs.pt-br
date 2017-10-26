---
title: "Como é usada de metadados? | Microsoft Docs"
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
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4723b48732065ccc2f307d9eeef46f8b35574c2d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="how-is-metadata-used"></a>Como é usada de metadados?
Os aplicativos exigem metadados para a maioria das operações de conjunto de resultados. Por exemplo, o aplicativo usa o tipo de dados de uma coluna para determinar que tipo de variável associar a essa coluna. Ele usa o comprimento em bytes de uma coluna de caracteres para determinar quanto espaço ele precisa para exibir dados da coluna. Como um aplicativo determina os metadados para uma coluna depende do tipo do aplicativo.  
  
 Aplicativos verticais trabalhar com tabelas predefinidas e executam operações predefinidas nessas tabelas. Como os metadados do conjunto de resultados para tais aplicativos é definido antes do aplicativo ainda foi criado e é controlado pelo desenvolvedor do aplicativo, pode ser embutido no aplicativo. Por exemplo, se uma coluna de ID de pedido for definida como um número inteiro de 4 bytes na fonte de dados, o aplicativo poderá sempre associar um número inteiro de 4 bytes a essa coluna. Quando os metadados forem embutidos em código no aplicativo, uma alteração nas tabelas usadas pelo aplicativo geralmente indica uma alteração no código do aplicativo. Isso raramente é um problema, porque geralmente são feitas alterações como parte de uma nova versão do aplicativo.  
  
 Como aplicativos verticais, os aplicativos personalizados geralmente funcionam com tabelas predefinidas e executam operações predefinidas nessas tabelas. Por exemplo, um aplicativo pode ser escrito para transferir dados entre três fontes de dados diferentes; os dados a serem transferidos normalmente são conhecidos quando o aplicativo é escrito. Assim, os aplicativos personalizados também tendem a ter metadados embutida.  
  
 Aplicativos genéricos, especialmente aqueles que oferecem suporte a consultas ad hoc, quase nunca saber os metadados dos conjuntos de resultados que eles criam. Portanto, eles devem descobrir os metadados em tempo de execução usando as funções **SQLNumResultCols**, **SQLDescribeCol**, e **SQLColAttribute**, que estão descritas as próxima seção, [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todos os aplicativos, independentemente de seu tipo, podem embutir metadados para os conjuntos de resultados retornados pelas funções de catálogo. Esses conjuntos de resultados são definidos na seção de referência deste manual.

