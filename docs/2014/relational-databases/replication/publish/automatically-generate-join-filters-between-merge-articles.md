---
title: Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66c32615b3fd9f417eab27f156b2645c2c89593b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63020972"
---
# <a name="automatically-generate-a-set-of-join-filters-between-merge-articles-sql-server-management-studio"></a>Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem (SQL Server Management Studio)
  Gere automaticamente um conjunto de filtros de junção na página **Filtrar Linhas da Tabela** no Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades de Publicação – \<Publicação>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Se você gerar automaticamente um conjunto de filtros de junção na caixa de diálogo **Propriedades de Publicação – \<Publicação>** após assinaturas à publicação terem sido inicializadas, deverá gerar um novo instantâneo e reinicializar todas as assinaturas após a alteração. Para obter mais informações sobre os requisitos para alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md).  
  
 Os filtros de junção podem ser criados manualmente para um conjunto de tabelas ou a replicação pode gerar os filtros automaticamente com base em relações de chave estrangeira para chave primária definidas nas tabelas. Para obter mais informações sobre como criar filtros de junção manualmente, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](define-and-modify-a-join-filter-between-merge-articles.md).  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>Para automaticamente gerar um conjunto de filtros de junção entre artigos de mesclagem  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades de Publicação – \<Publicação>** , clique em **Adicionar** e, em seguida, clique em **Gerar Filtros Automaticamente**.  
  
    > [!NOTE]  
    >  Gerando filtros automaticamente exclui quaisquer filtros de linha ou filtros de junção existentes na publicação. Você pode adicionar filtros depois de gerar um conjunto de filtros automaticamente.  
  
2.  Siga o processo na caixa de diálogo **Gerar Filtros** para criar um filtro de linha. O filtro de linha é então estendido para as tabelas relacionadas à tabela filtrada por relações de chave primária e de chave estrangeira.  
  
    1.  Selecione a tabela a ser filtrada a partir da caixa de listagem suspensa.  
  
    2.  Crie uma instrução de filtro na caixa de texto **Instrução de filtro** . Você pode digitar diretamente na área de texto e também pode arrastar e soltar colunas da caixa de listagem **Colunas** .  
  
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
  
         Selecione a opção que corresponde ao modo em que os dados serão compartilhados entre Assinantes: **Uma linha desta tabela irá para várias assinaturas** ou **uma linha desta tabela irá para apenas uma assinatura**. Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     O filtro que você especificou é analisado e executado na tabela, na cláusula SELECT. Se a instrução de filtro contiver erros de sintaxe ou outros problemas, você será notificado e poderá editar a instrução do filtro.  
  
     Depois de a instrução ser analisada, a replicação cria os filtros de junção necessários e os mostra no painel **Tabelas Filtradas** na página **Filtrar Linhas** de **Tabela ou Filtrar Linhas** . Se você estiver gerando filtros a partir do Assistente para Novas Publicações e ainda não tiver configurado o Distribuidor para o Publicador ao qual o assistente está sendo executado, será solicitado a fazer a configuração.  
  
4.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>Para modificar um filtro que foi gerado automaticamente  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades da Publicação – \<Publicação>** , selecione um filtro no painel **Tabelas Filtradas** e clique em **Editar**.  
  
2.  Na caixa de diálogo do **Editar Filtro** ou **Editar Junção** , modifique o filtro.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>Para excluir um filtro que foi gerado automaticamente  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** de **Propriedades da Publicação – \<Publicação>** , selecione um filtro no painel **Tabelas Filtradas** e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Join Filters](../merge/join-filters.md)   
 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
