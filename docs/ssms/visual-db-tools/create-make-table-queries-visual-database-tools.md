---
title: Criar consultas Criar Tabela (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3062cf684505e7c67c5b65a8e296ff75deb3610b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="create-make-table-queries-visual-database-tools"></a>Criar consultas Criar Tabela (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode copiar linhas em uma tabela nova utilizando uma consulta Criar Tabela, que é útil para criar subconjuntos de dados para trabalhar ou copiar o conteúdo de uma tabela de um banco de dados para outro. Uma consulta Criar Tabela é semelhante a uma consulta Inserir Resultados, porém cria uma nova tabela para copiar as linhas.  
  
Ao criar uma consulta Criar Tabela, você especifica:  
  
-   O nome da nova tabela de banco de dados (a tabela de destino).  
  
-   A tabela ou as tabelas de banco de dados de onde copiar as linhas (a tabela de origem). Você pode copiar de uma única tabela ou de tabelas unidas.  
  
-   As colunas da tabela de origem cujo conteúdo você deseja copiar.  
  
-   A ordem de classificação, se você desejar copiar as linhas em uma ordem específica.  
  
-   Os critérios de pesquisa para definir as linhas que você deseja copiar.  
  
-   As opções Agrupar por, se você quiser copiar somente resumos informativos.  
  
Por exemplo, a seguinte consulta cria uma nova tabela chamada `uk_customers` e copia informações da tabela `customers`:  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
Para usar uma consulta Criar Tabela com êxito:  
  
-   Seu banco de dados deve oferecer suporte à sintaxe SELECT...INTO.  
  
-   Você deve ter permissão para criar uma tabela no banco de dados de destino.  
  
### <a name="to-create-a-make-table-query"></a>Para criar uma consulta Criar Tabela  
  
1.  Adicione a tabela ou as tabelas de origem ao painel Diagrama.  
  
2.  No menu **Designer de Consultas** , aponte para **Alterar Tipo**e clique em **Criar Tabela**.  
  
3.  Na caixa de diálogo **Criar Tabela** , digite o nome da tabela de destino. O Designer de Consulta e Exibição não verifica se o nome já está em uso ou se você tem permissão para criar a tabela.  
  
    Para criar uma tabela de destino em outro banco de dados, especifique um nome de tabela totalmente qualificado incluindo o nome do banco de dados de destino, o proprietário (se necessário) e o nome da tabela.  
  
4.  Especifique as colunas a serem copiadas adicionando-as à consulta. Para obter detalhes, veja [Adicionar colunas a consultas (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md). As colunas só serão copiadas se você as adicionar à consulta. Para copiar linhas inteiras, escolha **\&#42; (Todas as Colunas)**.  
  
    O Designer de Consulta e Exibição adiciona as colunas escolhidas à coluna **Coluna** do painel Critérios.  
  
5.  Se você quiser copiar as linhas em uma ordem específica, selecione a ordem de classificação. Para obter detalhes, consulte **Classificação e agrupamento de resultados de consultas**.  
  
6.  Especifique as linhas a serem copiadas inserindo critérios de pesquisa. Para obter detalhes, veja [Especificar critérios de pesquisa (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Se você não especificar um critério de pesquisa, todas as linhas da tabela de origem serão copiadas na tabela de destino.  
  
    > [!NOTE]  
    > Quando você insere uma coluna para ser pesquisada no painel Critérios, o Designer de Consulta e Exibição também a adiciona à lista de colunas a serem copiadas. Se você quiser utilizar uma coluna para fazer uma pesquisa, mas não quiser copiá-la, desmarque a caixa de seleção próxima ao nome da coluna no retângulo que representa a tabela ou o objeto estruturado por tabela.  
  
7.  Para copiar resumos informativos, especifique as opções Agrupar por. Para obter detalhes, consulte [Resumir resultados da consulta (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md).  
  
Quando você executa a consulta Criar Tabela, nenhum resultado é relatado no painel de [Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Em vez disso, será exibida uma mensagem indicando o total de linhas copiadas.  
  
## <a name="see-also"></a>Consulte também  
[Tópicos de instruções de como criar consultas e exibições (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipos de consultas (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
