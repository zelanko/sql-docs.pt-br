---
title: Concluir trechos Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology:
- database-engine
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 968d9a6b20851970463bffa34d07863e86c2a7c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="complete-transact-sql-snippets"></a>Concluir trechos de código Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Quando um trecho de código [!INCLUDE[tsql](../../includes/tsql-md.md)] foi inserido em um script, você edita o conteúdo do trecho para compilar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] completa.  
  
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
  
  
