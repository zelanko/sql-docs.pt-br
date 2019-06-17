---
title: 'Como fazer: executar uma consulta parcial | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0dff2087286035b078f59ac1673a733fb3cc8358
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090171"
---
# <a name="how-to-execute-a-partial-query"></a>Como fazer: Executar uma consulta parcial
O Editor Transact\-SQL permite que você realce um segmento específico do script e execute-o como uma única consulta. Isto facilita a depuração de seções de consultas complexas.  
  
> [!WARNING]  
> O procedimento a seguir usa entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-partially-execute-a-query"></a>Para executar uma consulta parcialmente  
  
1.  No **Pesquisador de Objetos do SQL Server**, clique duas vezes em **PerishableFruits** em **Modos de Exibição** para abrir no editor Transact\-SQL.  
  
2.  Realce o segmento `SELECT p.Id, p.Name FROM dbo.Product p` no código, clique com o botão direito do mouse nele e selecione **Executar Consulta**.  
  
3.  Observe que todas as linhas com os campos especificados na tabela `Products` são retornadas no painel **Resultados**.  
  
