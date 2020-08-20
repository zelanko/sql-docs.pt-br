---
description: Como os metadados são usados?
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
ms.openlocfilehash: ca61677b0001ba4c39f81f80f6e3cbce26f27910
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476628"
---
# <a name="how-is-metadata-used"></a>Como os metadados são usados?
Os aplicativos exigem metadados para a maioria das operações de conjunto de resultados. Por exemplo, o aplicativo usa o tipo de dados de uma coluna para determinar que tipo de variável associar a essa coluna. Ele usa o comprimento em bytes de uma coluna de caracteres para determinar quanto espaço ele precisa para exibir dados dessa coluna. Como um aplicativo determina os metadados para uma coluna depende do tipo do aplicativo.  
  
 Os aplicativos verticais funcionam com tabelas predefinidas e executam operações predefinidas nessas tabelas. Como os metadados do conjunto de resultados para esses aplicativos são definidos antes de o aplicativo ser gravado e controlado pelo desenvolvedor do aplicativo, ele pode ser embutido no aplicativo. Por exemplo, se uma coluna de ID de pedido for definida como um número inteiro de 4 bytes na fonte de dados, o aplicativo poderá sempre associar um número inteiro de 4 bytes a essa coluna. Quando os metadados forem embutidos em código no aplicativo, uma alteração nas tabelas usadas pelo aplicativo geralmente indica uma alteração no código do aplicativo. Isso raramente é um problema, pois essas alterações geralmente são feitas como parte de uma nova versão do aplicativo.  
  
 Assim como os aplicativos verticais, os aplicativos personalizados geralmente funcionam com tabelas predefinidas e executam operações predefinidas nessas tabelas. Por exemplo, um aplicativo pode ser gravado para transferir dados entre três fontes de dados diferentes; os dados a serem transferidos geralmente são conhecidos quando o aplicativo é gravado. Assim, os aplicativos personalizados também tendem a ter metadados embutidos em código.  
  
 Aplicativos genéricos, especialmente aqueles que dão suporte a consultas ad hoc, quase nunca conhecem os metadados dos conjuntos de resultados que eles criam. Portanto, eles devem descobrir os metadados em tempo de execução usando as funções **SQLNumResultCols**, **SQLDescribeCol**e **SQLColAttribute**, que são descritas na próxima seção, [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todos os aplicativos, independentemente de seu tipo, podem embutir em código metadados para os conjuntos de resultados retornados pelas funções de catálogo. Esses conjuntos de resultados são definidos na seção de referência deste manual.
