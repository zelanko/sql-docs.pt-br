---
title: Filtrar linhas da tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.filtertablerows.f1
ms.assetid: 005f5c71-0401-490e-8823-adc54a2e9675
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eafa0dc2be5ee9ceffd86185399168589fdd8b1f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721224"
---
# <a name="filter-table-rows"></a>Filtrar Linhas da Tabela
  A página **Filtrar Linhas da Tabela** permite:  
  
-   Aplicar filtros de linhas estáticos a artigos de tabela em publicações de instantâneo, transacional e de mesclagem.  
  
-   Aplicar filtros de linha com parâmetros a artigos de tabela em publicações de mesclagem.  
  
-   Usar filtros de junção para estender filtros em artigos de tabela de mesclagem para artigos de tabela relacionados.  
  
 Para obter mais informações sobre opções de filtragem, consulte [Filter Published Data](publish/filter-published-data.md) (Filtrar dados publicados). A filtragem pode ser alterada na página **Filtrar Linhas** da caixa de diálogo **Propriedades de Publicação** .  
  
 Para maximizar o desempenho do aplicativo e reduzir a quantidade de uma armazenagem remota requerida ou restringir a disponibilidade de certos dados a Assinantes específicos, somente os dados requeridos devem ser publicados. Sua publicação pode incluir as tabelas filtradas e não filtradas. Por exemplo, você pode incluir a tabela completa (não filtrada) de produtos da empresa e usar filtros de linha para fornecer uma tabela filtrada aos clientes de uma região específica. Filtrando dados publicados, você pode:  
  
-   Minimizar a quantidade de dados enviada pela rede.  
  
-   Reduzir a quantidade de espaço de armazenamento requerida no Assinante.  
  
-   Personalizar publicações e aplicativos com base em requisitos de Assinante individuais.  
  
-   Evitar ou reduzir conflitos se o Assinante estiver atualizando dados, porque partições diferentes de dados podem ser enviadas a Assinantes diferentes (dois Assinantes não estarão atualizando os mesmos valores de dados).  
  
-   Evitar transmitir dados confidenciais. Podem ser usados filtros de linha e filtros de coluna para restringir um acesso de Assinante aos dados. Para a replicação de mesclagem, haverá considerações de segurança se você usar um filtro com parâmetros que inclua HOST_NAME(). Para obter mais informações, consulte a seção "Filtrando com HOST_NAME()" em [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
 Um filtro não deve incluir o `rowguidcol` usado por replicação para identificar linhas. Por padrão, esta é a coluna adicionada no momento que você define a replicação de mesclagem e é denominada **rowguid**.  
  
## <a name="options"></a>Opções  
 **Tabelas Filtradas**  
 Esse painel é populado com filtros à medida que são adicionados a artigos de tabela na publicação. Tabelas com filtros de linha são mostradas como nós de alto nível no painel. Para publicações de mesclagem, tabelas para as quais a filtragem foi estendida através de um filtro de junção são mostradas como nós filhos.  
  
 **Adicionar**  
 Clique em **Adicionar** para iniciar uma caixa de diálogo que permite filtrar artigos de tabela. Clicar em **Adicionar** para um instantâneo ou uma publicação transacional inicia imediatamente uma caixa de diálogo. Clicar em **Adicionar** para uma publicação de mesclagem exibe três opções: **Adicionar Filtro**; **Adicionar Junção para Estender o Filtro Selecionado**; **Gerar Filtros Automaticamente**.  
  
-   Selecione **Adicionar Filtro** para iniciar a caixa de diálogo **Adicionar filtro** . Essa caixa de diálogo permite aplicar filtros de linha a um artigo de tabela. Na caixa de diálogo **Adicionar Filtro** você pode, por exemplo, especificar que uma tabela com dados de cliente só contenha dados de clientes franceses quando for replicada para Assinantes.  
  
-   Selecione **Adicionar Junção para Estender o Filtro Selecionado** para iniciar a caixa de diálogo **Adicionar Junção** . A caixa de diálogo **Adicionar Junção** permite estender um filtro de linha para que filtre linhas em tabelas relacionadas à tabela com filtro de linha. Por exemplo, se uma tabela de cliente for filtrada para que contenha apenas dados de clientes franceses e houver uma tabela relacionada para pedidos de clientes, você pode definir uma junção entre as duas tabelas para que a tabela de pedidos só inclua pedidos de clientes franceses.  
  
    > [!NOTE]  
    >  Essa opção só estará disponível se você selecionar primeiro  a tabela base da junção no painel de filtro.  
  
-   Selecione **Gerar Filtros Automaticamente** para iniciar a caixa de diálogo **Gerar Filtros** . Essa caixa de diálogo permite definir um filtro de linha em uma tabela em uma publicação de mesclagem para que a replicação se estenda automaticamente a outras tabelas relacionadas por relações de chave estrangeira. Por exemplo, uma publicação pode incluir três tabelas: uma tabela de cliente, uma tabela de pedidos (com uma chave estrangeira para a tabela de cliente), e uma tabela de detalhes do pedido (com uma chave estrangeira para a tabela de pedidos). Defina um filtro de linha na tabela de cliente e replicação o estenderá às outras tabelas.  
  
    > [!NOTE]  
    >  Quando os filtros são gerados automaticamente por replicação, qualquer filtro existente na publicação é excluído. Para incluir os filtros gerados automaticamente e um especificado manualmente, gere os filtros primeiro. Você só pode especificar um conjunto de filtros gerado automaticamente para cada publicação.  
  
 **Editar**  
 Selecione um filtro de linha ou um filtro de junção no painel de filtros e clique em **Editar** para iniciar a caixa de diálogo **Editar Filtro** ou **Editar Junção** .  
  
 **Delete (excluir)**  
 Selecione um filtro de linha ou um filtro de junção no painel de filtro e clique em **Excluir** para excluir o filtro.  
  
 **Localizar Tabela**  
 Mescle publicações apenas com filtros de junção. Clique em **Localizar Tabela** para localizar uma tabela em uma árvore de filtro complexa. Em um banco de dados com relações complexas, pode haver junção de uma tabela com várias tabelas e, portanto, ela pode aparecer em mais de um lugar na árvore de filtro.  
  
 A tabela real só aparece em um lugar na árvore; em outros lugares a tabela é representada por um atalho. Um atalho para uma tabela é somente uma referência à tabela; ele não mostra os nós filhos da tabela. Um nó de atalho é marcado com uma seta de atalho e expandir esse nó mostra o texto **Clique em localizar tabela para ver a tabela \<tablename>** .  
  
 Selecione um nó de atalho no painel e clique em **Localizar Tabela**. O painel é expandido e a tabela é destacada. Se você clicar em **Localizar Tabela** sem um nó de atalho selecionado, uma caixa de diálogo **Localizar Tabela** será ativada.  
  
 **Filter**  
 Contém a definição [!INCLUDE[tsql](../../includes/tsql-md.md)] para o filtro selecionado no painel de filtro.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Filtrar os dados publicados](publish/filter-published-data.md)   
 [Join Filters](merge/join-filters.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)  
  
  
