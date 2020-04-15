---
title: Status somente leitura (Driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304017"
---
# <a name="read-only-status-excel-driver"></a>Status somente leitura (Driver do Excel)
Quando o driver do Microsoft Excel é usado, as tabelas de origem de dados são abertas apenas como leitura por padrão e podem ser abertas por apenas um usuário por vez. No entanto, embora as tabelas tenham status somente de leitura, os aplicativos podem realizar inserções e atualizações para tabelas do Microsoft Excel.  
  
 Quando um aplicativo executa um comando Save As nos dados do Microsoft Excel através do driver microsoft excel, o aplicativo deve criar uma nova tabela e inserir os dados a serem salvos na nova tabela. As inserções resultam em um apêndice na tabela. Nenhuma outra operação pode ser realizada na mesa até que seja fechada e reaberta. Uma vez fechada a tabela, nenhuma inserção subseqüente pode ser realizada porque a tabela é então uma tabela somente para leitura.  
  
 É possível atualizar valores ao usar o driver microsoft excel, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel, portanto, as atualizações não são consideradas oficialmente suportadas pelo driver do Microsoft Excel.
