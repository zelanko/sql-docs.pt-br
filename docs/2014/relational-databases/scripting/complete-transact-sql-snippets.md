---
title: Concluir snippets Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e1e6438128398b0210da20f68efcd88bb2f6eec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092566"
---
# <a name="complete-transact-sql-snippets"></a>Concluir snippets Transact-SQL
  Quando um snippet de código [!INCLUDE[tsql](../../includes/tsql-md.md)] foi inserido em um script, você edita o conteúdo do snippet para compilar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] completa.  
  
## <a name="completing-snippets"></a>Concluindo snippets  
 Quando você acrescentar um snippet [!INCLUDE[tsql](../../includes/tsql-md.md)] ao seu script, a instrução de snippet inserida terá um ou mais pontos de substituição, que serão destacados. Se você posicionar o seu ponteiro do mouse em um ponto de substituição, uma dica de ferramenta aparecerá com uma descrição do elemento de sintaxe que você pode especificar. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] Editor de Consulta reconhece o snippet como separado do script ao redor até que você feche o arquivo de origem. Os pontos de substituição permanecem ativos até que você feche o arquivo de origem.  
  
 Você também pode acrescentar elementos de sintaxe adicionais ao código de modelo inserido por um snippet. Por exemplo, o modelo Criar Snippet de Tabela gera duas definições de coluna; você deve adicionar outras definições de coluna para criar uma tabela com mais de duas colunas.  
  
#### <a name="completing-the-snippet-statement"></a>Concluindo a instrução de snippet  
  
1.  Use a tecla TAB para se mover de um ponto de substituição ao próximo. Use SHIFT+TAB para se mover para o ponto de substituição anterior.  
  
2.  Clique em CTRL+SPACE para invocar IntelliSense.  
  
3.  Selecione um item da lista ou digite uma substituição de sua escolha.  
  
## <a name="see-also"></a>Consulte também  
 [Inserir snippets Transact-SQL](insert-transact-sql-snippets.md)   
 [Inserir snippets Transact-SQL com Surround](insert-surround-with-transact-sql-snippets.md)  
  
  
