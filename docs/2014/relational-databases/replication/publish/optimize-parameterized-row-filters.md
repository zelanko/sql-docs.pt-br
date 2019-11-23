---
title: Otimizar filtros de linha com parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- filters [SQL Server replication], parameterized
- merge replication precomputed partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], optimizing
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 216504cc6145a60e8b7d4996d29f46cb9d08458d
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882144"
---
# <a name="optimize-parameterized-row-filters"></a>Otimizar filtros de linha com parâmetros
  Este tópico descreve como otimizar filtros de linha com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para otimizar filtros de linha com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Quando você usar filtros com parâmetros, será possível controlar como os filtros serão processados pela replicação de mesclagem, especificando a opção **use partition groups** ou a opção **keep partition changes** ao criar uma publicação. Essas opções melhoram o desempenho de sincronização para publicações com artigos filtrados, armazenando metadados adicionais no banco de dados de publicação. Você pode controlar como os dados serão compartilhados entre Assinantes definindo as **opções de partição** ao criar um artigo. Para obter mais informações sobre esses requisitos, consulte [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
     Com os assinantes do [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact, keep_partition_changes deve ser definido como true para assegurar que as exclusões sejam propagadas corretamente. Quando definido como falso, o assinante pode ter mais linhas do que o esperado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 As configurações seguintes podem ser usadas para aperfeiçoar filtros de linha com parâmetros:  
  
 **Partition Options**  
 Defina essa opção na página **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>** ou na caixa de diálogo **Adicionar Filtro**. Ambas as caixas de diálogo estão disponíveis no Assistente para Nova Publicação e na caixa de diálogo **Propriedades da Publicação – \<Publicação>** . A caixa de diálogo **Propriedades do Artigo – \<Artigo>** permite especificar valores adicionais para essa opção que não estão disponíveis na caixa de diálogo **Adicionar Filtro**.  
  
 **Pré-calcular partições**  
 Essa opção é definida, por padrão, para **True** se os artigos em sua publicação aderem a um conjuntos de requisitos. Para obter mais informações sobre esses requisitos, consulte [Otimizar o desempenho de filtro com parâmetros com partições pré-computadas](../merge/parameterized-filters-optimize-for-precomputed-partitions.md). Modifique essa opção na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>** .  
  
 **Otimizar sincronização**  
 Essa opção deve ser definida como **True** somente se **Pré-calcular Partições** estiver definida como **False**. Defina essa opção na página **Opções de Assinatura** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** .  
  
 Para obter mais informações sobre como usar o Assistente para Nova Publicação e acessar a caixa de diálogo **Propriedades da Publicação – \<Publicação>** , consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
#### <a name="to-set-partition-options-in-the-add-filter-or-edit-filter-dialog-box"></a>Para definir as opções de partição na caixa de diálogo Adicionar Filtro ou Editar Filtro  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **Adicionar** e, em seguida, em **Adicionar Filtro**.  
  
2.  Criar um filtro com parâmetros. Para obter mais informações, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
3.  Selecione a opção que corresponde ao modo em que os dados serão compartilhados entre Assinantes:  
  
    -   **Uma linha dessa tabela irá para múltiplas assinaturas**  
  
    -   **Uma linha dessa tabela irá para apenas uma assinatura**  
  
     Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-set-partition-options-in-the-article-properties---article-dialog-box"></a>Para definir as Opções de Partição na caixa de diálogo Propriedades do Artigo – \<Artigo>  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir Propriedades do Artigo Realçado na Tabela** ou **Definir as Propriedades de Todos os Artigos de Tabela**.  
  
3.  Na seção **Objeto de Destino** da guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>** , especifique um dos seguintes valores para **Opções de Partição**:  
  
    -   **Com sobreposição**  
  
    -   **Com sobreposição, não permitir alterações de dados fora da partição**  
  
    -   **Sem-sobreposição, única assinatura**  
  
    -   **Sem-sobreposição, compartilhados entre assinaturas**  
  
     Para obter mais informações sobre essas opções e sobre como estão relacionadas às opções disponíveis nas caixas de diálogo **Adicionar Filtro** e **Editar Filtro** , consulte a seção "Definindo as opções de partição'" em [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-set-precompute-partitions"></a>Para definir o Pré-calcular Partições  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione um valor para a opção **Pré-calcular Partições**. A propriedade é somente leitura se:  
  
    -   A publicação não satisfizer os requisitos para as partições pré-calculadas.  
  
    -   Um instantâneo ainda não tiver sido gerado para a publicação. Nesse caso, a opção exibe um valor de **Definir automaticamente quando um instantâneo é criado.**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-optimize-synchronization"></a>Para definir o Otimizar Sincronização  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione o valor **True** para a opção **Otimizar Sincronização**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Para obter definições das opções de filtragem para **\@keep_partition_changes** e **\@use_partition_groups**, consulte [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql).  
  
#### <a name="to-specify-merge-filter-optimizations-when-creating-a-new-publication"></a>Para especificar otimizações de filtro de mesclagem ao criar uma nova publicação  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique **\@publicação** e um valor de `true` para um dos seguintes parâmetros:  
  
    -   **\@use_partition_groups**:-a otimização de desempenho mais alta, desde que os artigos estejam em conformidade com os requisitos para partições preputadas. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
    -   **\@keep_partition_changes** -Use essa otimização se partições computadas não puderem ser usadas.  
  
2.  Adicione um trabalho de instantâneo para a publicação. Para obter mais informações, consulte [Criar uma publicação](create-a-publication.md).  
  
3.  No Publicador do banco de dados de publicação, execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), especificando os seguintes parâmetros:  
  
    -   **\@publicação** -o nome da publicação da etapa 1.  
  
    -   **\@artigo** -um nome para o artigo  
  
    -   **\@source_object** -o objeto de banco de dados que está sendo publicado.  
  
    -   **\@subset_filterclause** -a cláusula de filtro com parâmetros opcional usada para filtrar horizontalmente o artigo.  
  
    -   **\@partition_options** -as opções de partição para o artigo filtrado.  
  
4.  Repita a etapa 3 para cada artigo na publicação.  
  
5.  (Opcional) No Assinante do banco de dados de publicação, execute [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) para definir um filtro de junção entre dois artigos. Para obter mais informações, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](define-and-modify-a-join-filter-between-merge-articles.md).  
  
#### <a name="to-view-and-modify-merge-filter-behaviors-for-an-existing-publication"></a>Para visualizar e modificar comportamentos de filtro de mesclagem para uma publicação existente  
  
1.  Adicional No Publicador do banco de dados de publicação, execute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), especificando **\@publicação**. Observe o valor de **keep_partition_changes** e **use_partition_groups** no conjunto de resultados.  
  
2.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique um valor de **use_partition_groups** para a **propriedade\@** e `true` ou `false` para o **valor de\@** .  
  
3.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique um valor de **keep_partition_changes** para a **propriedade\@** e `true` ou `false` para o **valor de\@** .  
  
    > [!NOTE]  
    >  Ao habilitar **keep_partition_changes**, primeiro você deve desabilitar **use_partition_groups** e especificar um valor de **1** para **\@force_reinit_subscription**.  
  
4.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **partition_options** para a **Propriedade\@** e o valor apropriado para **\@valor**. Consulte [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definições destas opções de filtragem.  
  
5.  (Opcional) Iniciar o Snapshot Agent para regenerar o instantâneo se necessário. Para obter informações sobre quais alterações exigem a criação de um novo instantâneo, consulte [Alterar as propriedades da publicação e do artigo](change-publication-and-article-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem &#40;SQL Server Management Studio&#41;](automatically-generate-join-filters-between-merge-articles.md)   
 [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtros de linha com parâmetros](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
