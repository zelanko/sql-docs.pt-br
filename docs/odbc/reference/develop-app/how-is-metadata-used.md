---
title: Como os metadados são usados? | Microsoft Docs
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
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbbba96fa2e99a2ccc0618f31e3b29e7d479f703
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300166"
---
# <a name="how-is-metadata-used"></a>Como os metadados são usados?
Os aplicativos exigem metadados para a maioria das operações de conjunto de resultados. Por exemplo, o aplicativo usa o tipo de dados de uma coluna para determinar que tipo de variável associar a essa coluna. Ele usa o comprimento do byte de uma coluna de caracteres para determinar quanto espaço ele precisa para exibir dados dessa coluna. Como um aplicativo determina os metadados para uma coluna depende do tipo do aplicativo.  
  
 As aplicações verticais funcionam com tabelas predefinidas e realizam operações predefinidas nessas tabelas. Como os metadados definidos por resultados para tais aplicativos são definidos antes mesmo de o aplicativo ser escrito e é controlado pelo desenvolvedor do aplicativo, ele pode ser codificado no aplicativo. Por exemplo, se uma coluna de ID de pedido for definida como um número inteiro de 4 bytes na fonte de dados, o aplicativo poderá sempre associar um número inteiro de 4 bytes a essa coluna. Quando os metadados forem embutidos em código no aplicativo, uma alteração nas tabelas usadas pelo aplicativo geralmente indica uma alteração no código do aplicativo. Isso raramente é um problema, porque essas alterações geralmente são feitas como parte de uma nova versão do aplicativo.  
  
 Como aplicativos verticais, aplicativos personalizados geralmente funcionam com tabelas predefinidas e executam operações predefinidas nessas tabelas. Por exemplo, um aplicativo pode ser escrito para transferir dados entre três fontes de dados diferentes; os dados a serem transferidos são geralmente conhecidos quando o aplicativo é escrito. Assim, aplicativos personalizados também tendem a ter metadados codificados.  
  
 Aplicativos genéricos, especialmente aqueles que suportam consultas ad hoc, quase nunca conhecem os metadados dos conjuntos de resultados que criam. Portanto, eles devem descobrir os metadados em tempo de execução usando as funções **SQLNumResultCols,** **SQLDescribeCol**e **SQLColAttribute,** que são descritas na próxima seção, [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todos os aplicativos, independentemente do seu tipo, podem codificar metadados para os conjuntos de resultados retornados pelas funções do catálogo. Estes conjuntos de resultados são definidos na seção de referência deste manual.
