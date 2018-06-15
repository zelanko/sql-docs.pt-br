---
title: Status de somente leitura (Driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d885124c9e4274d402bfa504b975f089d333af95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32900521"
---
# <a name="read-only-status-excel-driver"></a>Status de somente leitura (Driver do Excel)
Quando o driver do Microsoft Excel é usado, as tabelas de origem de dados abertas como somente leitura por padrão e podem ser abertas somente por um usuário por vez. Mesmo que as tabelas que o status de somente leitura, no entanto, aplicativos podem executar as inserções e atualizações para tabelas do Microsoft Excel.  
  
 Quando um aplicativo executa um comando Salvar como em dados do Microsoft Excel através do driver do Microsoft Excel, o aplicativo deve criar uma nova tabela e insira os dados sejam salvos na nova tabela. Inserções resultam em um acrescentar à tabela. Nenhuma outra operação pode ser executada na tabela até que ele é fechado e reaberto. Quando a tabela for fechada, nenhuma inserção subsequente pode ser executada porque a tabela, em seguida, é uma tabela somente leitura.  
  
 É possível atualizar os valores ao usar o driver do Microsoft Excel, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel, para que as atualizações são considerados não oferecerá suporte para o driver do Microsoft Excel.
