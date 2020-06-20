---
title: 'Lição 5: automatizando a limpeza e a correspondência usando o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 90f967b2446e11a27f5a87803bb71d6e1ec53557
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039839"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>Lição 5: Automatizando a limpeza e a correspondência usando o SSIS
  Na lição 1, você criou a base de dados de conhecimento dos fornecedores e a usou para limpar os dados na lição 2 e corresponder dados na lição 3 usando a ferramenta **cliente do DQS**. Em um cenário do mundo real, pode ser necessário extrair dados de uma fonte que o DQS não suporta ou você deseja automatizar o processo de limpeza e correspondência sem precisar usar a ferramenta de **cliente do DQS** . O SQL Server Integration Services (SSIS) tem componentes que você pode usar para integrar dados de várias fontes heterogêneas e um componente de **[transformação de limpeza DQS](https://msdn.microsoft.com/library/ee677619.aspx)** para invocar a funcionalidade de limpeza exposta pelo DQS. Atualmente, o DQS não expõe a funcionalidade correspondente para uso do SSIS, mas você pode usar a **[transformação Agrupamento Difuso](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** para identificar duplicatas nos dados.  
  
 Você pode carregar dados para o MDS usando o **recurso de preparo baseado em entidade**. Quando você cria uma entidade no MDS, os procedimentos armazenados e as tabelas de preparo correspondentes são criados automaticamente. Por exemplo, quando você criou a entidade Supplier, a tabela **STG. supplier_Leaf** e o procedimento armazenado **STG. udp_Supplier_Leaf** foram criados automaticamente. Use os procedimentos e as tabelas de preparo para criar, atualizar e excluir membros de entidade. Nesta lição, você criará novos membros de entidade para a Entidade Fornecedor. Para carregar dados no servidor MDS, o pacote SSIS primeiro carrega os dados na tabela de preparação stg.supplier_Leaf e, em seguida, dispara o procedimento armazenado stg.udp_Supplier_Leaf associado. Consulte [importando dados](../master-data-services/overview-importing-data-from-tables-master-data-services.md) para obter mais detalhes.  
  
 Nesta lição, você executará as seguintes tarefas:  
  
1.  Remover dados do fornecedor no MDS (se você tiver feito as quatro lições anteriores). O pacote SSIS criado nessa lição carrega automaticamente os dados no MDS. Antigamente, você carregava manualmente os dados limpos e correspondentes do fornecedor no servidor MDS usando o Cliente DQS.  
  
2.  Criar uma exibição de assinatura na entidade Fornecedor para expor os dados da entidade a outros aplicativos. Essa ação cria uma exibição SQL que você verificará usando o SQL Server Management Studio. Você não utilizará essa exibição nesta versão do tutorial.  
  
3.  Crie e execute um projeto do SSIS usando **SQL Server Data Tools**. O projeto usa a transformação **limpeza de dados** para enviar uma solicitação de limpeza ao servidor DQS. O DQS ainda não expõe a funcionalidade correspondente, portanto, você usará a transformação **Agrupamento Difuso** para identificar duplicatas.  
  
4.  Verificar se os dados foram criados no MDS usando o Master Data Manager.  
  
5.  Examinar os resultados do projeto de limpeza DQS criado pelo pacote SSIS e, se desejar, executar a limpeza interativa para criar a base de dados de conhecimento posteriormente.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 1 &#40;pré-requisito&#41;: removendo dados do fornecedor no MDS](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
