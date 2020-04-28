---
title: Status somente leitura (driver do Excel) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304017"
---
# <a name="read-only-status-excel-driver"></a>Status somente leitura (Driver do Excel)
Quando o driver do Microsoft Excel é usado, as tabelas de fontes de dados são abertas como somente leitura por padrão e podem ser abertas por apenas um usuário por vez. Embora as tabelas tenham status somente leitura, no entanto, os aplicativos podem executar inserções e atualizações para tabelas do Microsoft Excel.  
  
 Quando um aplicativo executa um comando Salvar como nos dados do Microsoft Excel por meio do driver do Microsoft Excel, o aplicativo deve criar uma nova tabela e inserir os dados a serem salvos na nova tabela. Inserções resultam em um acréscimo à tabela. Nenhuma outra operação pode ser executada na tabela até que ela seja fechada e reaberta. Depois que a tabela é fechada, nenhuma inserção subsequente pode ser executada porque a tabela é, então, uma tabela somente leitura.  
  
 É possível atualizar valores ao usar o driver do Microsoft Excel, mas uma linha não pode ser excluída de uma tabela baseada em uma planilha do Microsoft Excel, portanto, as atualizações não são consideradas oficialmente suportadas pelo driver do Microsoft Excel.
