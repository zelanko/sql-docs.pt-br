---
title: Status de somente leitura (Driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: d0cdfec3129dbe01e5b25f0c8595b8bd4e528ba8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="read-only-status-excel-driver"></a>Status de somente leitura (Driver do Excel)
Quando o driver do Microsoft Excel é usado, as tabelas de origem de dados abertas como somente leitura por padrão e podem ser abertas somente por um usuário por vez. Mesmo que as tabelas que o status de somente leitura, no entanto, aplicativos podem executar as inserções e atualizações para tabelas do Microsoft Excel.  
  
 Quando um aplicativo executa um comando Salvar como em dados do Microsoft Excel através do driver do Microsoft Excel, o aplicativo deve criar uma nova tabela e insira os dados sejam salvos na nova tabela. Inserções resultam em um acrescentar à tabela. Nenhuma outra operação pode ser executada na tabela até que ele é fechado e reaberto. Quando a tabela for fechada, nenhuma inserção subsequente pode ser executada porque a tabela, em seguida, é uma tabela somente leitura.  
  
 É possível atualizar os valores ao usar o driver do Microsoft Excel, mas uma linha não pode ser excluída de uma tabela com base em uma planilha do Microsoft Excel, para que as atualizações são considerados não oferecerá suporte para o driver do Microsoft Excel.
