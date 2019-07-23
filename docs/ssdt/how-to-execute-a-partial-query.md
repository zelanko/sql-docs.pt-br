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
ms.openlocfilehash: 2f7861e3ef232dd3f244c9c325468e6ba4d51d16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929618"
---
# <a name="how-to-execute-a-partial-query"></a>Como fazer: Executar uma consulta parcial
O Editor Transact\-SQL permite que você realce um segmento específico do script e execute-o como uma única consulta. Isto facilita a depuração de seções de consultas complexas.  
  
> [!WARNING]  
> O procedimento a seguir usa entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-partially-execute-a-query"></a>Para executar uma consulta parcialmente  
  
1.  No **Pesquisador de Objetos do SQL Server**, clique duas vezes em **PerishableFruits** em **Modos de Exibição** para abrir no editor Transact\-SQL.  
  
2.  Realce o segmento `SELECT p.Id, p.Name FROM dbo.Product p` no código, clique com o botão direito do mouse nele e selecione **Executar Consulta**.  
  
3.  Observe que todas as linhas com os campos especificados na tabela `Products` são retornadas no painel **Resultados**.  
  
