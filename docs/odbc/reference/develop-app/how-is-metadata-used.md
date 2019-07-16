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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab2efd47ca5b5492c67b88261795cf524c440bda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139005"
---
# <a name="how-is-metadata-used"></a>Como os metadados são usados?
Os aplicativos exigem metadados para a maioria das operações de conjunto de resultados. Por exemplo, o aplicativo usa o tipo de dados de uma coluna para determinar que tipo de variável associar a essa coluna. Ele usa o comprimento em bytes de uma coluna de caracteres para determinar quanto espaço que ele precisa exibir dados dessa coluna. Como um aplicativo determina os metadados para uma coluna depende do tipo do aplicativo.  
  
 Aplicativos verticais trabalhar com tabelas predefinidas e executam operações predefinidas nessas tabelas. Como os metadados do conjunto de resultados para tais aplicativos é definido antes do aplicativo ainda foi criado e é controlado pelo desenvolvedor do aplicativo, pode ser embutido em código no aplicativo. Por exemplo, se uma coluna de ID de pedido for definida como um número inteiro de 4 bytes na fonte de dados, o aplicativo poderá sempre associar um número inteiro de 4 bytes a essa coluna. Quando os metadados forem embutidos em código no aplicativo, uma alteração nas tabelas usadas pelo aplicativo geralmente indica uma alteração no código do aplicativo. Isso raramente é um problema, porque essas alterações geralmente são feitas como parte de uma nova versão do aplicativo.  
  
 Assim como aplicativos verticais, aplicativos personalizados geralmente funcionam com tabelas predefinidas e executam operações predefinidas nessas tabelas. Por exemplo, um aplicativo pode ser escrito para transferir dados entre três diferentes fontes de dados; os dados a serem transferidos geralmente são conhecidos quando o aplicativo é escrito. Assim, aplicativos personalizados também tendem a ter metadados embutido em código.  
  
 Aplicativos genéricos, especialmente aquelas que dão suporte a consultas ad hoc, os metadados dos conjuntos de resultados que eles criam quase nunca se sabe. Portanto, eles devem descobrir os metadados em tempo de execução usando as funções **SQLNumResultCols**, **SQLDescribeCol**, e **SQLColAttribute**, que são descritos no próxima seção, [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Todos os aplicativos, independentemente de seu tipo, podem embutir metadados para os conjuntos de resultados retornados pelas funções de catálogo. Esses conjuntos de resultados são definidos na seção de referência deste manual.
