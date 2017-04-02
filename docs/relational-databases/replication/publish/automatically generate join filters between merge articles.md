---
title: "Gerar automaticamente um conjunto de filtros de jun&#231;&#227;o entre artigos de mesclagem (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "geração de filtro de junção automática"
  - "filtros de junção"
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Gerar automaticamente um conjunto de filtros de jun&#231;&#227;o entre artigos de mesclagem (SQL Server Management Studio)
  Gerar automaticamente um conjunto de filtros de junção no **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Se você gerar automaticamente um conjunto de filtros de junção no **Propriedades de publicação - \< publicação>** caixa de diálogo depois que tiverem sido inicializadas assinaturas para a publicação, você deve gerar um novo instantâneo e reinicializar todas as assinaturas após fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Os filtros de junção podem ser criados manualmente para um conjunto de tabelas ou a replicação pode gerar os filtros automaticamente com base em relações de chave estrangeira para chave primária definidas nas tabelas. Para obter mais informações sobre como criar filtros de junção manualmente, consulte [definir e modificar uma junção filtro entre mesclar artigos](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
### Para automaticamente gerar um conjunto de filtros de junção entre artigos de mesclagem   
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, clique em **Add**, e, em seguida, clique em **Gerar filtros automaticamente**.  
  
    > [!NOTE]  
    >  Gerando filtros automaticamente exclui quaisquer filtros de linha ou filtros de junção existentes na publicação. Você pode adicionar filtros depois de gerar um conjunto de filtros automaticamente.  
  
2.  Siga o processo no **Gerar filtros** caixa de diálogo para criar um filtro de linha. O filtro de linha é então estendido para as tabelas relacionadas à tabela filtrada por relações de chave primária e de chave estrangeira.  
  
    1.  Selecione a tabela a ser filtrada a partir da caixa de listagem suspensa.  
  
    2.  Crie uma instrução de filtro no **instrução de filtro** caixa de texto. Você pode digitar diretamente na área de texto e também pode arrastar e soltar colunas da caixa de listagem **Colunas** .  
  
         A área de texto **Instrução de filtro** inclui o texto padrão que está no formato de:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         O texto padrão não pode ser alterado; digite a cláusula do filtro para um filtro de linha estático ou um filtro de linha com parâmetros após a palavra chave WHERE usando a sintaxe SQL padrão. A cláusula de filtro completa para um filtro de linha com parâmetros teria este formato:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         A cláusula WHERE deve usar nomeação de duas partes; nomeação de três partes e nomeação de quatro partes não são suportadas.  
  
    3.  Especifique as opções de filtro.  
  
         Selecione a opção que corresponde a como os dados serão compartilhados entre assinantes: **uma linha dessa tabela irá para múltiplas assinaturas** ou **uma linha dessa tabela irá para apenas uma assinatura**. Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     O filtro que você especificou é analisado e executado na tabela, na cláusula SELECT. Se a instrução de filtro contiver erros de sintaxe ou outros problemas, você será notificado e poderá editar a instrução do filtro.  
  
     Depois que a instrução é analisada, a replicação cria os filtros de junção necessários e os exibe no **tabelas filtradas** Painel de **Filtrar linhas da tabela** ou **Filtrar linhas** página. Se você estiver gerando filtros a partir do Assistente para Novas Publicações e ainda não tiver configurado o Distribuidor para o Publicador ao qual o assistente está sendo executado, será solicitado a fazer a configuração.  
  
4.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
### Para modificar um filtro que foi gerado automaticamente  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Editar**.  
  
2.  No **Editar filtro** ou **Editar junção** caixa de diálogo caixa, modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para excluir um filtro que foi gerado automaticamente  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>**, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Excluir**.  
  
## Consulte também  
 [Filtros de junção](../../../relational-databases/replication/merge/join-filters.md)   
 [Filtros de linha com parâmetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  