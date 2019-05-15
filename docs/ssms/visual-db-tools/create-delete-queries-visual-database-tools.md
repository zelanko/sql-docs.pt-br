---
title: Criar consultas de exclusão (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- row removal [SQL Server], Delete query
- Delete query
- queries [SQL Server], types
- removing rows
- removing data
- data deletions [SQL Server]
- deleting rows
- deleting data
ms.assetid: 0db3af43-1ec4-48c8-b769-2bb9c76d3434
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 40b9dd59f70243dcfd547c8a94ca8b46f3237ddf
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089511"
---
# <a name="create-delete-queries-visual-database-tools"></a>Criar consultas de exclusão (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode excluir todas as linhas em uma tabela usando uma consulta Exclusão.  
  
> [!NOTE]  
> A exclusão de todas as linhas da tabela limpa os dados na tabela, mas não exclui a tabela em si. Para excluir uma tabela de um banco de dados, clique com o botão direito do mouse na tabela no Pesquisador de Objetos e clique em **Excluir**.  
  
Quando você cria uma consulta Exclusão, o painel Critérios é alterado para refletir as opções disponíveis para exclusão de linhas. Como não são exibidos dados na consulta Exclusão, as colunas Saída, Classificar por e Ordem de Classificação são removidas. Além disso, as caixas de seleção próximas aos nomes de coluna no retângulo que representa a tabela ou o objeto com valor de tabela são removidas, pois você não pode especificar colunas individuais para exclusão.  
  
Se o Designer de Consulta e Exibição não puder excluir uma ou mais linhas, nenhuma delas será excluída e você receberá uma mensagem informando quais linhas contêm informações que não podem ser excluídas do banco de dados.  
  
> [!CAUTION]  
> Você não pode desfazer a ação de execução da consulta Exclusão. Como precaução, faça backup de seus dados antes de executar uma consulta Exclusão.  
  
### <a name="to-create-a-delete-query"></a>Para criar uma consulta Exclusão  
  
1.  Adicione a tabela para excluir linhas no painel Diagrama.  
  
2.  No menu **Designer de Consultas** , aponte para **Alterar Tipo**e clique em **Excluir**. **Observação** Se mais de uma tabela for exibida no painel Diagrama quando você iniciar a consulta de Exclusão, o Designer de Consulta e Exibição exibirá a caixa de diálogo [Excluir Tabela](../../ssms/visual-db-tools/delete-table-dialog-box-visual-database-tools.md) , que solicitará o nome da tabela cujas linhas serão excluídas.  
  
Quando você executa a consulta de Exclusão, nenhum resultado é relatado no [Painel de Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Em vez disso, é exibida uma mensagem indicando quantas linhas foram excluídas.  
  
## <a name="see-also"></a>Consulte Também  
[Tipos de consulta com suporte &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
