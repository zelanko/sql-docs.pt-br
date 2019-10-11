---
title: Filtros de linha com parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], dynamic filters
- merge replication [SQL Server replication], dynamic filters
- parameterized filters [SQL Server replication]
- filters [SQL Server replication], dynamic
- merge replication parameterized filters [SQL Server replication]
- publications [SQL Server replication], parameterized filters
- parameterized filters [SQL Server replication], about parameterized filters
- filters [SQL Server replication], parameterized
- dynamic filters [SQL Server replication]
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3dee5b4c6522afd93591d1e8aa0c94052d41d9bd
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71711063"
---
# <a name="parameterized-filters---parameterized-row-filters"></a>Filtros com parâmetros – Filtros de linha com parâmetros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os filtros de linha com parâmetros permitem que diferentes partições de dados sejam enviadas a diferentes Assinantes sem a necessidade de criar múltiplas publicações (os filtros com parâmetros foram referidos como filtros dinâmicos em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]). Uma partição é um subconjunto das linhas de uma tabela; dependendo das configurações escolhidas ao criar um filtro de linha com parâmetros, cada linha de uma tabela publicada pode pertencer a uma partição somente (o que produz partições que não se sobrepõem) ou a duas ou mais partições (o que produzem partições que se sobrepõem).  
  
 Partições que não se sobrepõem podem ser compartilhadas entre assinaturas ou podem ser restringidas de modo que só uma assinatura receba uma determinada partição. As configurações que controlam comportamento de partição são descritas em "Usando opções de filtragem apropriadas", mais adiante neste tópico. Usando essas configurações você pode personalizar a filtragem com parâmetros de acordo com o aplicativo e os requisitos de desempenho. Em geral, partições que se sobrepõem permitem maior flexibilidade e partições que não se sobrepõem replicadas a uma única assinatura proporcionam melhor desempenho.  
  
 Os filtros com parâmetros são usados em uma única tabela e normalmente são combinados com filtros de junção para estender a filtragem a tabelas relacionadas. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
 Para definir ou modificar um filtro de linha com parâmetros, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
## <a name="how-parameterized-filters-work"></a>Como funcionam os filtros com parâmetros  
 Um filtro de linha com parâmetros usa uma cláusula WHERE para selecionar os dados apropriados a serem publicados. Em vez de especificar um valor literal na cláusula (como você faria com um filtro de linha estático), você especifica uma das seguintes funções do sistema ou ambas: SUSER_SNAME() e HOST_NAME(). Funções definidas pelo usuário também podem ser usadas, mas devem incluir SUSER_SNAME() ou HOST_NAME() no corpo da função, ou avaliar uma dessas funções de sistema (como `MyUDF(SUSER_SNAME()`). Se uma função definida pelo usuário incluir SUSER_SNAME() ou HOST_NAME() no corpo da função, você não pode passar parâmetros para a função.  
  
 As funções de sistema SUSER_SNAME() e HOST_NAME() não são específicas para replicação de mesclagem, mas são usadas para por replicação de mesclagem para filtragem com parâmetros:  
  
-   SUSER_SNAME() retorna informações de logon para conexões feitas a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando usado em um filtro com parâmetros, esse retorna o logon utilizado pelo Agente de Mesclagem para fazer a conexão com o Publicador (você pode especificar um logon ao criar uma assinatura).  
  
-   HOST_NAME() retorna o nome do computador que está se conectando a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ao usar um filtro com parâmetros, por padrão este retorna o nome do computador no qual o Agente de Mesclagem está sendo executado. Para assinaturas pull, este é o nome do Assinante; para assinaturas push, é o nome do Distribuidor.  
  
     Também é possível substituir essa função com um valor que não seja o nome do Assinante ou do Distribuidor. Normalmente, os aplicativos substituem essa função com valores mais significativos, tais como um nome de vendedor ou uma identificação de vendedor. Para obter mais informações, consulte a seção "Substituindo o valor de HOST_NAME()" neste tópico.  
  
 O valor retornado pela função do sistema é comparado a uma coluna que você especifica na tabela que está filtrando, e os dados apropriados são baixados para o Assinante. Essa comparação é feita quando a assinatura é inicializada (de modo que apenas os dados apropriados estejam contidos no instantâneo inicial) e a cada vez que a assinatura é sincronizada. Por padrão, se uma alteração no Publicador fizer com que uma linha seja removida de uma partição, a linha será excluída do Assinante (esse comportamento é controlado com o uso do parâmetro `@allow_partition_realignment` de [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)).  
  
> [!NOTE]  
>  Quando são feitas comparações para filtros com parâmetros, a ordenação de banco de dados sempre é usada. Por exemplo, se a ordenação de banco de dados não diferencia maiúsculas e minúsculas, mas a ordenação de tabela ou coluna o faz, a comparação não diferenciará maiúsculas e minúsculas.  
  
### <a name="filtering-with-suser_sname"></a>Filtrando com SUSER_SNAME()  
 Considere a **Tabela de Funcionários** no banco de dados de exemplo [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] . Essa tabela inclui a coluna **LoginID**, que contém o login para cada funcionário na forma '*domain\login*'. Para filtrar essa tabela de modo que os funcionários recebam só os dados relacionados a eles, especifique uma cláusula de filtro de:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Por exemplo, o valor para um dos funcionários é 'adventure-works\john5'. Quando o Agente de Mesclagem faz a conexão com o Publicador, ele utiliza o logon especificado na criação da assinatura (neste caso, 'adventure-works\john5'). O Agente de Mesclagem então compara o valor retornado por SUSER_SNAME() com os valores na tabela e baixa apenas a linha que contenha um valor de 'adventure-works\john5' na coluna **LoginID** .  
  
### <a name="filtering-with-host_name"></a>Filtrando com HOST_NAME()  
 Considere a tabela **HumanResources.Employee** . Suponha que essa tabela contenha uma coluna tal como **ComputerName** com o nome de cada computador de funcionário na forma '*name_computertype*'. Para filtrar essa tabela de modo que os funcionários recebam só os dados relacionados a eles, especifique uma cláusula de filtro de:  
  
```  
ComputerName = HOST_NAME()  
```  
  
 Por exemplo, o valor para um dos funcionários poderia ser 'john5_laptop'. Quando o Agente de Mesclagem faz a conexão com o Publicador, ele compara o valor retornado por HOST_NAME() com os valores na tabela e baixa apenas a linha que contenha um valor de 'john5_laptop' na coluna **ComputerName** .  
  
 Também é possível combinar as funções em um filtro. Por exemplo, se você quisesse assegurar-se de que um funcionário recebeu os dados apenas se usou seu logon em seu computador, a cláusula do filtro poderia ser:  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 A menos que você esteja substituindo o valor HOST_NAME(), a filtragem com HOST_NAME() normalmente é usada somente com assinaturas pull. O valor retornado pela função é o nome do computador no qual o Agente de Mesclagem está sendo executado. Para assinaturas pull, o valor é diferente para cada assinatura; para assinaturas push, porém, o valor é o mesmo (todos os Agente de Mesclagems são executados no Distribuidor para assinaturas push).  
  
> [!IMPORTANT]  
>  O valor para a função HOST_NAME() pode ser substituído; portanto não é possível usar filtros que incluam HOST_NAME() para controlar o acesso a partições de dados. Para controlar o acesso a partições de dados, use SUSER_SNAME(), SUSER_SNAME() em combinação com HOST_NAME(), ou use filtros de linha estáticos.  
  
#### <a name="overriding-the-host_name-value"></a>Substituindo o valor HOST_NAME()  
 Como observado anteriormente, HOST_NAME() por padrão retorna o nome do computador que está se conectando a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ao usar filtros com parâmetros, é comum substituir esse valor fornecendo um valor ao criar uma assinatura. Uma função HOST_NAME() retorna o valor que você especifica em lugar do nome do computador.  
  
> [!NOTE]  
>  Se substituir HOST_NAME(), todas as chamadas para a função HOST_NAME() retornarão o valor que você especificou. Assegure-se de que outros aplicativos não estão dependendo de que HOST_NAME() retorne o nome do computador.  
  
 Considere a tabela **HumanResources.Employee** . Essa tabela inclui a coluna **EmployeeID**. Para filtrar essa tabela de modo que cada funcionário receba só os dados relacionados a ele, especifique uma cláusula de filtro de:  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 Por exemplo, a funcionária Pamela Ansman-Wolfe recebeu uma identificação de funcionário 280. Especifique o valor da identificação de funcionário (280 em nosso exemplo) para o valor HOST_NAME() ao criar uma assinatura para essa funcionária. Quando o Agente de Mesclagem faz a conexão com o Publicador, ele compara o valor retornado por HOST_NAME() com os valores na tabela e baixa apenas a linha que contém um valor 280 na coluna **EmployeeID** .  
  
> [!IMPORTANT]
>  A função HOST_NAME() retorna um valor **nchar** , e por isso você deve usar CONVERT se a coluna na cláusula de filtro for de tipo de dados numéricos, como no exemplo acima. Por razões de desempenho, recomendamos não aplicar funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, tais como `CONVERT(nchar,EmployeeID) = HOST_NAME()`. Em vez disso, recomendamos usar a abordagem mostrada no exemplo: `EmployeeID = CONVERT(int,HOST_NAME())`. Essa cláusula pode ser usada para o parâmetro `@subset_filterclause` de [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), mas ela geralmente não pode ser usada no Assistente de Nova Publicação (o assistente executa a cláusula de filtro para validá-la, o que não acontece por que o nome do computador não poder ser convertido em um **int**). Se você usar o Assistente de Nova Publicação, recomendamos especificar `CONVERT(nchar,EmployeeID) = HOST_NAME()` no assistente e usar [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) para alterar a cláusula para `EmployeeID = CONVERT(int,HOST_NAME())` antes de criar um instantâneo para a publicação.  
  
 **Para substituir o valor HOST_NAME()**  
  
 Use um dos métodos seguintes para substituir o valor HOST_NAME():  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: especifique um valor na página **Valores de HOST\_NAME\(\)** do Assistente de Nova Assinatura. Para obter mais informações sobre como criar assinaturas, consulte [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Programação [!INCLUDE[tsql](../../../includes/tsql-md.md)] de replicação: especifique um valor para o parâmetro `@hostname` de [sp_addmergesubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) (para assinaturas push) ou de [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (para assinaturas pull).  
  
-   Agente de Mesclagem: especifique um valor para o parâmetro **-Hostname** na linha de comando ou por meio de um perfil de agente. Para obter mais informações sobre o Agente de Mesclagem, consulte [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md). Para obter mais informações sobre perfis de agente, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="initializing-a-subscription-to-a-publication-with-parameterized-filters"></a>Inicializando uma assinatura para uma publicação com filtros com parâmetros  
 Quando são usados filtros de linha com parâmetros em publicações de mesclagem, a replicação inicializa cada assinatura com um instantâneo de duas partes. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="using-the-appropriate-filtering-options"></a>Usando as opções de filtragem apropriadas  
 Há duas áreas-chaves sobre as quais você tem controle ao usar filtros com parâmetros:  
  
-   Como os filtros são processados por replicação de mesclagem, que é controlada por uma das duas configurações de publicação: **usar grupos de partição** e **manter alterações de partição**.  
  
-   Como os dados são compartilhados entre Assinantes, o que deve ser refletido pela configuração de artigo **opções de partição**.  
  
 Para definir opções de filtragem, consulte [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md).  
  
### <a name="setting-use-partition-groups-and-keep-partition-changes"></a>Definindo 'usar grupos de partição’ e 'manter alterações de partição’  
 Tanto a opção **usar grupos de partição** quanto a opção **manter alterações de partição** melhoram o desempenho de sincronização para publicações com artigos filtrados, por armazenarem metadados adicionais no banco de dados de publicação. A opção **usar grupos de partição** proporciona maior melhoria de desempenho pelo uso do recurso de partições pré-computadas. Essa opção é por padrão definida como **true** se os artigos em sua publicação obedecem a um conjunto de requisitos. Para obter mais informações sobre esses requisitos, consulte [Otimizar o desempenho de filtro com parâmetros com partições pré-computadas](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md). Se seus artigos não satisfizerem os requisitos para uso de partições pré-computadas, a opção **manter alterações de partição** é definida como **true**.  
  
### <a name="setting-partition-options"></a>Definindo 'opções de partição’  
 Você especifica um valor para a propriedade **opções de partição** ao criar um artigo, de acordo com a maneira em que os dados na tabela filtrada serão compartilhados pelos Assinantes. A propriedade pode ser definida com um dentre quatro valores usando [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)e a caixa de diálogo **Propriedades do Artigo** . A propriedade pode ser definida com um dentre dois valores usando as caixas de diálogo **Adicionar Filtro** ou **Editar Filtro** , que estão disponíveis no Assistente de Nova Publicação e na caixa de diálogo **Propriedades de Publicação** . A tabela a seguir resume os valores disponíveis:  
  
|Descrição|Valor em Adicionar filtro e Editar Filtro|Valor em Propriedades do Artigo|Valor em procedimentos armazenados|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|Os dados nas partições estão sobrepostos e o Assinante pode atualizar colunas referenciadas em um filtro com parâmetros.|**Uma linha dessa tabela irá para múltiplas assinaturas**|**Com sobreposição**|**0**|  
|Os dados nas partições estão sobrepostos e o Assinante não pode atualizar colunas referenciadas em um filtro com parâmetros.|N/A*|**Com sobreposição, não permitir alterações de dados fora da partição**|**1**|  
|Os dados nas partições não estão sobrepostos e os dados são compartilhados entre assinaturas. O Assinante não pode atualizar colunas referenciadas em um filtro com parâmetros.|N/A*|**Sem-sobreposição, compartilhados entre assinaturas**|**2**|  
|Os dados nas partições não estão sobrepostos e há uma única assinatura por partição. O Assinante não pode atualizar as colunas referenciadas em um filtro parametrizado.**|**Uma linha dessa tabela irá para apenas uma assinatura**|**Sem-sobreposição, única assinatura**|**3**|  
  
 \*Se a opção de filtragem subjacente for definida como **0**, **1** ou **2**, as caixas de diálogo **Adicionar Filtro** e **Editar Filtro** exibirão a mensagem **Uma linha dessa tabela irá para várias assinaturas**.  
  
 **Se você especificar esta opção, somente poderá haver uma única assinatura para cada partição de dados nesse artigo. Se uma segunda assinatura for criada na qual o critério de filtragem da nova assinatura for resolvido para a mesma partição como a assinatura existente, a assinatura existente será cancelada.  
  
> [!IMPORTANT]  
>  O valor **opções de partição** deve ser definido de acordo com a maneira como os dados são compartilhados pelos Assinantes. Se, por exemplo, você especificar que uma partição é sem-sobreposição com uma assinatura única por partição, mas os dados forem então atualizados em outro Assinante, o Agente de Mesclagem poderá não funcionar durante a sincronização e poderá ocorrer uma não convergência.  
  
#### <a name="selecting-the-appropriate-partition-option"></a>Selecionando a opção de partição apropriada  
 Partições que não se sobrepõem funcionam em conjunção com partições pré-computadas para melhorar o desempenho em situações em que algumas limitações funcionais sejam aceitáveis. As partições pré-computadas aceleram os downloads para Assinantes, mas retardam os carregamentos. Partições que não se sobrepõem minimizam o custo de carregamento associado a partições pré-computadas. O benefício de desempenho de partições que não se sobrepõem é mais notável quando os filtros com parâmetros e de junção usados são mais complexos.  
  
 Considere os cenários seguintes ao decidir que opções de partição usar em uma publicação.  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] dispõe de uma força de vendas móvel em cada vendedor responsável por clientes em um determinado código postal. O aplicativo requer que o código postal seja atualizado se um cliente se muda de um território de vendas para outro, de maneira o cliente que seja atribuído a um vendedor diferente. O filtro com parâmetros tem como base o código postal do cliente e a atualização remove o código postal da partição de um vendedor e insere-o na partição de outro vendedor. Isso requer partições que se sobreponham e que possam atualizar colunas referenciadas em um filtro com parâmetros. Essa opção maximiza a flexibilidade, mas poderia não ter desempenho tão bom quanto partições que não se sobrepõem.  
  
-   Uma agência de empregos tem dados que são fornecidos a escritórios regionais em cada município do estado. Os dados não se sobrepõem; cada linha na tabela para a matriz do órgão está incluída em apenas uma partição, mas esta partição é enviada a escritórios múltiplos no mesmo município. A opção de partição que não se sobrepõe, com partições compartilhadas entre assinaturas, é apropriada, proporcionando uma melhoria de desempenho, se comparada com a partições que se sobrepõem, e ao mesmo tempo satisfazem os requisitos do aplicativo.  
  
-   Se você tiver partições que não se sobrepõem e apenas uma assinatura recebe e atualiza os dados em uma partição, benefícios de desempenho adicionais podem ser obtidos. Esse cenário é comum para sistemas de pontos de vendas e aplicativos de força de vendas em que os dados são basicamente coletados no Assinante e carregados no Publicador. Considere uma tabela **Pacote** em um aplicativo de entrega: como cada pacote é carregado em um caminhão, o status do pacote é alterado na tabela **Pacote** , e a alteração é replicada de volta para a matriz. Os motoristas não atualizariam os status do mesmo pacote em dois caminhões diferentes, e por isso a tabela **Pacote** é uma boa candidata para uma partição que não se sobrepõe, com uma assinatura única por partição.  
  
#### <a name="considerations-for-nonoverlapping-partitions"></a>Considerações para partições que não se sobrepõem  
 Lembre-se das seguintes considerações ao usar partições que não se sobrepõem.  
  
##### <a name="general-considerations"></a>Considerações gerais  
  
-   A publicação deve usar partições pré-computadas.  
  
-   Uma linha deve pertencer a uma só partição.  
  
-   Artigos não podem fazer parte de um registro lógico.  
  
-   Não há suporte para parceiros de sincronização alternativos (esse recurso é preterido).  
  
-   O Assinante não pode atualizar colunas referenciadas em um filtro com parâmetros.  
  
-   Se uma inserção em um Assinante não pertencer à partição, não é excluída. Ela, porém, não será replicada a outros Assinantes.  
  
-   Em algumas circunstâncias com partições que se sobrepõem, os intervalos de identidade são ajustados quando o Agente de Mesclagem insere dados. Com partições que não se sobrepõem, os intervalos podem ser ajustados durante as inserções por um usuário que tenha permissão para ajustar intervalos de identidade no banco de dados de assinatura. O usuário deve possuir a tabela ou ser um membro da função de servidor fixa **sysadmin** , da função de banco de dados fixa **db_owner** ou da função de banco de dados fixa **db_ddladmin** .  
  
##### <a name="additional-considerations-for-nonoverlapping-partitions-with-a-single-subscription-per-partition"></a>Considerações adicionais para partições que não se sobrepõem com uma única assinatura por partição  
  
-   Os artigos podem estar presentes em apenas uma publicação; não podem ser republicados.  
  
-   A publicação deve permitir que os Assinantes iniciem o processo de instantâneo. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
##### <a name="additional-considerations-for-join-filters"></a>Considerações adicionais para filtros de junção  
  
-   Em uma hierarquia de filtros de junção, um artigo com uma partição que se sobrepõe não pode aparecer acima de um artigo com uma partição que não se sobrepõe. Em outras palavras, um artigo pai deve usar partições que não se sobrepõem se o artigo de filho as usar também. Para obter mais informações sobre filtros de junção, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Em um filtro de junção em que a partição que não se sobrepõe seja filho, a propriedade **juntar chave exclusiva** deve ser definida como 1. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   O artigo deve ter só um filtro com parâmetros ou filtro de junção. É permitido ter um filtro com parâmetros e ser o pai em um filtro de junção. Não é permitido ter um filtro com parâmetros e ser o filho em um filtro de junção. Também não é permitido ter mais que um filtro de junção.  
  
-   Se duas tabelas do Publicador tiverem uma relação de filtro de junção e a tabela filho tiver linhas que não tenham nenhuma linha correspondente na tabela pai, uma inserção da linha pai faltante não fará com que as linhas relacionadas sejam baixadas para o Assinante (as linhas seriam baixadas com partições que se sobrepusessem). Por exemplo, se a tabela **SalesOrderDetail** tiver linhas sem nenhuma linha correspondente na tabela **SalesOrderHeader** e você inserir a linhas faltante em **SalesOrderHeader**, a linha é baixada para o Assinante, mas as linhas correspondentes em **SalesOrderDetail** não o são.  
  
## <a name="see-also"></a>Consulte Também  
 [Melhores práticas para filtros de linha baseados em tempo](../../../relational-databases/replication/merge/best-practices-for-time-based-row-filters.md)   
 [Filtrar os dados publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrar dados publicados para a replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
