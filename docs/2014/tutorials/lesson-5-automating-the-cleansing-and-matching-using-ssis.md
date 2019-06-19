---
title: 'Lição 5: Automatizando a limpeza e correspondência usando o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f068d4db-2d56-41b1-bed2-0cffa3ca411d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ec6f347cdbc6d14e8f621466a1708b8ee9fe7d36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489749"
---
# <a name="lesson-5-automating-the-cleansing-and-matching-using-ssis"></a>Lição 5: Como automatizar a limpeza e a correspondência usando o SSIS
  Na lição 1, você criou a base de dados de Conhecimento de fornecedores e usou para limpar dados na lição 2 e correspondência de dados na lição 3 usando a ferramenta **cliente DQS**. Em um cenário do mundo real, talvez você precise extrair dados de uma fonte que não oferece suporte a DQS ou você deseja automatizar a limpeza e o processo de correspondência sem precisar usar o **cliente DQS** ferramenta. SQL Server Integration Services (SSIS) tem componentes que você pode usar para integrar dados de várias fontes heterogêneas e uma **[transformação de limpeza DQS](https://msdn.microsoft.com/library/ee677619.aspx)** componente para invocar a limpeza funcionalidade exposta pelo DQS. Atualmente, o DQS não expõe a funcionalidade de correspondência para uso do SSIS, mas você pode usar o **[transformação agrupamento difuso](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)** para identificar duplicatas nos dados.  
  
 Você pode carregar dados no MDS usando o **recurso preparação baseada em entidade**. Quando você cria uma entidade no MDS, os procedimentos armazenados e as tabelas de preparo correspondentes são criados automaticamente. Por exemplo, quando criou a entidade fornecedor, o **supplier_leaf** tabela e o **udp_supplier_leaf** procedimento armazenado foram criadas automaticamente. Use os procedimentos e as tabelas de preparo para criar, atualizar e excluir membros de entidade. Nesta lição, você criará novos membros de entidade para a Entidade Fornecedor. Para carregar dados no servidor MDS, o pacote SSIS primeiro carrega os dados na tabela de preparação stg.supplier_Leaf e, em seguida, dispara o procedimento armazenado stg.udp_Supplier_Leaf associado. Ver [importando dados](../master-data-services/overview-importing-data-from-tables-master-data-services.md) para obter mais detalhes.  
  
 Nesta lição, você executará as seguintes tarefas:  
  
1.  Remover dados do fornecedor no MDS (se você tiver feito as quatro lições anteriores). O pacote SSIS criado nessa lição carrega automaticamente os dados no MDS. Antigamente, você carregava manualmente os dados limpos e correspondentes do fornecedor no servidor MDS usando o Cliente DQS.  
  
2.  Criar uma exibição de assinatura na entidade Fornecedor para expor os dados da entidade a outros aplicativos. Essa ação cria uma exibição SQL que você verificará usando o SQL Server Management Studio. Você não utilizará essa exibição nesta versão do tutorial.  
  
3.  Criar e executar um projeto do SSIS por meio **SQL Server Data Tools**. O projeto utiliza **limpeza de dados** transformação para enviar uma solicitação de limpeza para o servidor DQS. O DQS não expõe a funcionalidade de correspondência ainda, portanto, você usará **agrupamento difuso** transformação para identificar duplicatas.  
  
4.  Verificar se os dados foram criados no MDS usando o Master Data Manager.  
  
5.  Examinar os resultados do projeto de limpeza DQS criado pelo pacote SSIS e, se desejar, executar a limpeza interativa para criar a base de dados de conhecimento posteriormente.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 1 &#40;pré-requisitos&#41;: Removendo os dados do fornecedor no MDS](../../2014/tutorials/task-1-prerequisite-removing-supplier-data-in-mds.md)  
  
  
