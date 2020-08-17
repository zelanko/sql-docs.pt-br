---
description: Status somente leitura (Driver do Excel)
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
ms.openlocfilehash: 04a0c5d0cb2c9932d30c0edb900169d8c5e5f82b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340382"
---
# <a name="read-only-status-excel-driver"></a>Status somente leitura (Driver do Excel)
Quando o driver do Microsoft Excel é usado, as tabelas de fontes de dados são abertas como somente leitura por padrão e podem ser abertas por apenas um usuário por vez. Embora as tabelas tenham status somente leitura, no entanto, os aplicativos podem executar inserções e atualizações para tabelas do Microsoft Excel.  
  
 Quando um aplicativo executa um comando Salvar como nos dados do Microsoft Excel por meio do driver do Microsoft Excel, o aplicativo deve criar uma nova tabela e inserir os dados a serem salvos na nova tabela. Inserções resultam em um acréscimo à tabela. Nenhuma outra operação pode ser executada na tabela até que ela seja fechada e reaberta. Depois que a tabela é fechada, nenhuma inserção subsequente pode ser executada porque a tabela é, então, uma tabela somente leitura.  
  
 É possível atualizar valores ao usar o driver do Microsoft Excel, mas uma linha não pode ser excluída de uma tabela baseada em uma planilha do Microsoft Excel, portanto, as atualizações não são consideradas oficialmente suportadas pelo driver do Microsoft Excel.
