---
title: Concluir trechos Transact-SQL | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3762aa8a27e9b3607b218024256418c480ff454
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="complete-transact-sql-snippets"></a>Concluir trechos de código Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Quando um trecho de código [!INCLUDE[tsql](../../includes/tsql-md.md)] foi inserido em um script, você edita o conteúdo do trecho para compilar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] completa.  
  
## <a name="completing-snippets"></a>Concluindo trechos  
 Quando você acrescentar um trecho [!INCLUDE[tsql](../../includes/tsql-md.md)] ao seu script, a instrução de trecho inserida terá um ou mais pontos de substituição, que serão destacados. Se você posicionar o seu ponteiro do mouse em um ponto de substituição, uma dica de ferramenta aparecerá com uma descrição do elemento de sintaxe que você pode especificar. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] Editor de Consulta reconhece o trecho como separado do script ao redor até que você feche o arquivo de origem. Os pontos de substituição permanecem ativos até que você feche o arquivo de origem.  
  
 Você também pode acrescentar elementos de sintaxe adicionais ao código de modelo inserido por um trecho. Por exemplo, o modelo Criar Trecho de Tabela gera duas definições de coluna; você deve adicionar outras definições de coluna para criar uma tabela com mais de duas colunas.  
  
#### <a name="completing-the-snippet-statement"></a>Concluindo a instrução de trecho  
  
1.  Use a tecla TAB para se mover de um ponto de substituição ao próximo. Use SHIFT+TAB para se mover para o ponto de substituição anterior.  
  
2.  Clique em CTRL+SPACE para invocar IntelliSense.  
  
3.  Selecione um item da lista ou digite uma substituição de sua escolha.  
  
## <a name="see-also"></a>Consulte Também  
 [Inserir trechos Transact-SQL](../../relational-databases/scripting/insert-transact-sql-snippets.md)   
 [Inserir trechos Transact-SQL com Surround](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
