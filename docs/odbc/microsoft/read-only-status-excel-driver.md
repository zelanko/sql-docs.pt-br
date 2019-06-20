---
title: Status de somente leitura (Driver do Excel) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17425e76814a8397b9d2e6167248f35e52ac6cfa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316742"
---
# <a name="read-only-status-excel-driver"></a>Status somente leitura (Driver do Excel)
Quando o driver do Microsoft Excel é usado, tabelas de fonte de dados abertas como somente leitura por padrão e podem ser abertas somente por um usuário por vez. Mesmo que as tabelas têm o status somente leitura, no entanto, aplicativos podem executar inserções e atualizações para tabelas do Microsoft Excel.  
  
 Quando um aplicativo executa um comando Salvar como em dados do Microsoft Excel através do driver do Microsoft Excel, o aplicativo deve criar uma nova tabela e inserir os dados a serem salvos na nova tabela. Inserções resultam em um acréscimo à tabela. Nenhuma outra operação pode ser executada na tabela até que ela é fechada e reaberta. Depois que a tabela for fechada, nenhuma subsequentes de inserção podem ser executada porque a tabela, em seguida, é uma tabela somente leitura.  
  
 É possível atualizar os valores ao usar o driver do Microsoft Excel, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel, para que as atualizações não são consideradas oficialmente com suporte pelo driver do Microsoft Excel.
