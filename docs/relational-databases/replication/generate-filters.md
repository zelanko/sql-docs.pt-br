---
description: Gerar Filtros
title: Gerar filtros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5c124642da9b895522e35c80e5edf68f50335dc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428028"
---
# <a name="generate-filters"></a>Gerar Filtros
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   A caixa de diálogo **Gerar Filtros** permite definir um filtro de linha em uma tabela em uma publicação de mesclagem; a replicação, então, estende automaticamente o filtro para outras tabelas relacionadas por relações de chave estrangeira. Por exemplo, se você definir um filtro em uma tabela de cliente para que contenha apenas dados de clientes franceses, a replicação estenderá esse filtro para que as tabelas de pedidos relacionadas e detalhes do pedidos contenham somente informações relacionadas aos clientes franceses.  
  
## <a name="options"></a>Opções  
 Essa caixa de diálogo envolve um processo de três etapas para criar um filtro de linha em uma tabela. O filtro é então estendido para as tabelas relacionadas à tabela filtrada por relações de chave primária e chave estrangeira. Por exemplo, nas três tabelas **Customer**, **SalesOrderHeader**e **SalesOrderDetail**, com uma relação entre **Customer** e **SalesOrderHeader**, e uma relação entre **SalesOrderHeader** e **SalesOrderDetail**, aplique um filtro de linha em **Customer**e a replicação estenderá esse filtro a **SalesOrderHeader** e **SalesOrderDetail**.  
  
1.  **Selecionar a tabela a ser filtrada**  
  
     Selecione uma tabela na caixa de listagem suspensa. As tabelas só serão exibidas na caixa de listagem se forem selecionadas na página **Artigos** .  
  
2.  **Conclua a instrução de filtro para identificar quais linhas de tabela os Assinantes receberão**  
  
     Defina uma nova instrução de filtro. A caixa de listagem **Colunas** lista todas as colunas que você está publicando da tabela selecionada em **Selecionar a tabela a ser filtrada**. A área de texto **Instrução de filtro** inclui o texto padrão que está no formato de:  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     Esse texto padrão não pode ser alterado; digite a cláusula de filtro depois da palavra-chave WHERE usando a sintaxe padrão [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    > [!IMPORTANT]  
    >  Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar HOST_NAME em uma cláusula de filtro e substituir o valor HOST_NAME, talvez precise converter tipos de dados usando CONVERT. Para obter mais informações sobre práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME()" no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Especifique quantas assinaturas receberão dados desta tabela**  

     Somente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Replicação de mesclagem permite especificar o tipo de partição que melhor combina com seus dados e aplicativo. Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem definirá a opção de partições não sobrepostas. Partições não sobrepostas funcionam com partições pré-computadas para melhorar o desempenho, com as partições não sobrepostas minimizando o custo de carregamento associado a partições pré-computadas. O benefício de desempenho de partições que não se sobrepõem é mais notável quando os filtros com parâmetros e de junção usados são mais complexos. Se você selecionar essa opção, deve assegurar que os dados sejam particionados de forma tal que uma linha não possa ser replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Depois de adicionar um filtro, clique em **OK** para sair e fechar a caixa de diálogo. O filtro que você especificou é analisado e executado na tabela, na cláusula SELECT. Se a instrução de filtro contiver erros de sintaxe ou outros problemas, você será notificado e poderá editar a instrução do filtro.  
  
 Depois que a instrução é analisada, a replicação cria os filtros de junção necessários. Se você ainda não tiver configurado o Distribuidor para o Publicador no qual este assistente está sendo executado, será solicitado a fazê-lo.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrar os dados publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
