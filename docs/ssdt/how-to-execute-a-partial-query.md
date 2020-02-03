---
title: Executar uma consulta parcial
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 5786127626a655e47e2f6eb4ba96f0a16b740258
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241422"
---
# <a name="how-to-execute-a-partial-query"></a>Como: Executar uma consulta parcial

O Editor Transact\-SQL permite que você realce um segmento específico do script e execute-o como uma única consulta. Isto facilita a depuração de seções de consultas complexas.  
  
> [!WARNING]  
> O procedimento a seguir usa entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
## <a name="to-partially-execute-a-query"></a>Para executar uma consulta parcialmente  
  
1. No **Pesquisador de Objetos do SQL Server**, clique duas vezes em **PerishableFruits** em **Modos de Exibição** para abrir no editor Transact\-SQL.  
  
2. Realce o segmento `SELECT p.Id, p.Name FROM dbo.Product p` no código, clique com o botão direito do mouse nele e selecione **Executar Consulta**.  
  
3. Observe que todas as linhas com os campos especificados na tabela `Products` são retornadas no painel **Resultados**.