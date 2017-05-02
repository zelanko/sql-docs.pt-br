---
title: Adicionar ou editar filtro | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7647baaaf9e567ada31eb468b6c48844676659f2
ms.lasthandoff: 04/11/2017

---
# <a name="add-or-edit-filter"></a>Adicionar ou Editar Filtro
  As caixas de diálogo **Adicionar Filtro** e **Editar Filtro** permitem adicionar e editar filtros de linhas estáticos e filtros de linhas com parâmetros.  
  
> [!NOTE]  
>  Editar um filtro em uma publicação existente requer um novo instantâneo para a publicação. Se uma publicação tiver assinaturas, as assinaturas deverão ser reiniciadas. Para obter mais informações sobre alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Todos os tipos de publicação podem incluir filtros estáticos; publicações de mesclagem também podem incluir filtros com parâmetros. Um filtro estático é avaliado quando a publicação é criada: todos os Assinantes da publicação recebem os mesmos dados. Um filtro com parâmetros é avaliado durante a sincronização de replicação: Assinantes diferentes podem receber partições diferentes de dados com base no logo ou nome de computador de cada Assinante. Clique no link **Exemplos de instruções** na caixa de diálogo para consultar exemplos de cada tipo de filtro. Para obter mais informações sobre opções de filtragem, consulte [Filter Published Data](../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
 Usando filtros de linha, você pode especificar um subconjunto de linhas a ser publicado de uma tabela. Filtros de linha podem ser usados para eliminar linhas que os usuários não precisam consultar (como linhas que contenham informações reservadas ou confidenciais), ou para criar partições diferentes de dados que são enviadas a diferentes Assinantes. A publicação de partições diferentes de dados para Assinantes diferentes também pode ajudar a evitar conflitos que de outra forma poderiam ser causados por vários Assinantes atualizando os mesmos dados.  
  
## <a name="options"></a>Opções  
 Essa caixa de diálogo envolve um processo de duas etapas para publicações transacional e de instantâneo e um processo de três etapas para publicações de mesclagem. Todo tipo de publicação requer que você selecione uma tabela a ser filtrada e uma ou mais colunas a serem incluídas no filtro; o filtro é definido como uma cláusula WHERE padrão.  
  
1.  **Selecione a tabela a ser filtrada**  
  
     Se você estiver editando um filtro existente, a seleção da tabela não poderá ser alterada. Se você estiver adicionando um novo filtro , selecione uma tabela na caixa de listagem suspensa. Tabelas só aparecem na caixa de listagem se foram selecionadas na página **Artigos** e ainda não têm um filtro de linha. Se uma tabela tiver um filtro de linha e você quer definir um novo:  
  
    1.  Clique em **Cancelar** na caixa de diálogo **Adicionar Filtro** .  
  
    2.  Selecione a tabela no painel de filtros, na página **Filtrar Linhas da Tabela** e clique em **Editar**.  
  
    3.  Edite um filtro existente na caixa de diálogo **Editar Filtro** .  
  
2.  **Conclua a instrução de filtro para identificar quais linhas de tabela os Assinantes receberão**  
  
     Defina uma nova instrução de filtro ou edite uma existente. A caixa de listagem **Colunas** lista todas as colunas que você está publicando da tabela selecionada em **Selecionar a tabela a ser filtrada**. A área de texto **Instrução de filtro** inclui o texto padrão que está no formato de:  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     Esse texto padrão não pode ser alterado; digite a cláusula de filtro depois da palavra-chave WHERE usando a sintaxe padrão [!INCLUDE[tsql](../../includes/tsql-md.md)] . Se o Editor for um Editor Oracle, a cláusula WHERE deve estar em conformidade com a sintaxe de consulta Oracle. Evite usar filtros complexos quando possível. Filtros estáticos e com parâmetros aumentam o tempo de processamento das publicações; portanto, mantenha as instruções de filtro o mais simples possível.  
  
    > [!IMPORTANT]  
    >  Por motivos de desempenho, recomendamos que não sejam aplicadas funções a nomes de colunas em cláusulas de filtros de linha com parâmetros, como `LEFT([MyColumn]) = SUSER_SNAME()`. Se você usar HOST_NAME em uma cláusula de filtro e substituir o valor HOST_NAME, talvez precise converter tipos de dados usando CONVERT. Para obter mais informações sobre práticas recomendadas para esse caso, consulte a seção "Substituindo o valor de HOST_NAME()" no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Especifique quantas assinaturas receberão dados desta tabela**  
  
     Somente[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores; somente replicação de mesclagem. Replicação de mesclagem permite especificar o tipo de partição que melhor combina com seus dados e aplicativo. Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem definirá a opção de partições não sobrepostas. Partições não sobrepostas funcionam com partições pré-computadas para melhorar o desempenho, com as partições não sobrepostas minimizando o custo de carregamento associado a partições pré-computadas. O benefício de desempenho de partições que não se sobrepõem é mais notável quando os filtros com parâmetros e de junção usados são mais complexos. Se você selecionar essa opção, deve assegurar que os dados sejam particionados de forma tal que uma linha não possa ser replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Depois de adicionar ou editar um filtro, clique em **OK** para salvar as alterações e fechar a caixa de diálogo. O filtro que você especificou é analisado e executado na tabela, na cláusula SELECT. Se a instrução de filtro contiver erros de sintaxe ou outros problemas, você será notificado e poderá editar a instrução de filtro.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrar os dados publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtros de junção](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
