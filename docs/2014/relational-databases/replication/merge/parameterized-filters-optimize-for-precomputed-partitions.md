---
title: Otimizar o desempenho de filtro com parâmetros com partições pré-computadas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication]
- merge replication precomputed partitions [SQL Server replication], about precomputed partitions
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8f80afa10c1dbd067648db26c2bed0f423f371b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250544"
---
# <a name="optimize-parameterized-filter-performance-with-precomputed-partitions"></a>Otimizar o desempenho de filtro parametrizado com partições pré-computadas
  Partições pré-computadas são uma otimização de desempenho que pode ser usada com publicações de mesclagem filtradas. Partições pré-computadas também são um requisito para usar registros lógicos em publicações filtradas. Para obter mais informações sobre registros lógicos, consulte [Agrupar alterações em linhas relacionadas com registros lógicos](group-changes-to-related-rows-with-logical-records.md).  
  
 Quando um Assinante faz a sincronização com um Publicador, este deve avaliar os filtros do Assinante para determinar quais linhas pertencem àquele Assinante ou conjunto de dados. Esse processo de determinação de associação de partição de alterações no Publicador para cada Assinante recebendo um conjunto de dados filtrado é referido como *avaliação de partição*. Sem partições pré-computadas, a avaliação de partição deve ser executada para cada alteração feita em uma coluna filtrada no Publicador desde a última vez que o Agente de Mesclagem foi executado em um Assinante específico e esse processo tem de ser repetido para cada Assinante que sincroniza com o Publicador.  
  
 Entretanto, se o Publicador e o Assinante estiverem sendo executados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou em uma versão posterior e você pode usar partições pré-computadas, a associação de partição de todas as alterações no Publicador será pré-computada e persistirá na hora que as alterações forem feitas. Como resultado, quando um Assinante sincroniza com o Publicador, ele pode começar imediatamente a baixar as alterações relevantes à sua partição sem ter de passar pelo processo de avaliação de partição. Isso pode levar a um ganho significativo de desempenho quando a publicação tem um grande número de alterações, Assinantes ou artigos na publicação.  
  
 Além de usar partições pré-computadas, instantâneos pré-gerados e/ou permitir que os Assinantes solicitem geração e aplicação de instantâneos na primeira vez que eles sincronizarem. Use uma, ou ambas as opções, para fornecer instantâneos para publicações que usam filtros com parâmetros. Se você não especificar uma dessas opções, as assinaturas serão inicializadas usando uma série de instruções SELECT e INSERT, ao invés de usar o utilitário **bcp** , esse processo é muito mais lento. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 **Para usar partições pré-computadas**  
  
 Partições de pré-computadas estão habilitadas, por padrão, em todas as publicações novas e existentes que aderem às diretrizes descritas acima. A configuração pode ser alterada pelo [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou programaticamente. Para obter mais informações, consulte [Optimize Parameterized Row Filters](../publish/optimize-parameterized-row-filters.md).  
  
## <a name="requirements-for-using-precomputed-partitions"></a>Requisitos para usar partições pré-computadas  
 Se os seguintes requisitos forem satisfeitos, novas publicações de mesclagem serão, por padrão, criadas com as partições pré-computadas habilitadas, e as publicações existentes serão automaticamente atualizadas para usar a característica. Se uma publicação não satisfizer os requisitos, ela poderá ser alterada e, então, as partições pré-computadas poderão ser habilitadas. Se alguns artigos satisfizerem os requisitos e outros não, considere criar duas publicações, sendo uma delas habilitada para partições pré-computadas.  
  
### <a name="requirements-for-filter-clauses"></a>Requisitos para cláusulas de filtro  
  
-   Quaisquer funções usadas em filtros de linha com parâmetros, como HOST_NAME() e SUSER_SNAME(), deveriam aparecer diretamente na cláusula de filtro com parâmetros e não ser aninhada dentro de uma exibição ou função dinâmica. Para obter mais informações sobre essas funções, consulte [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql), [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) e [Filtros de linha com parâmetros](parameterized-filters-parameterized-row-filters.md).  
  
-   Os valores retornados para cada Assinante não deveriam alterar depois que a partição seja criada. Por exemplo, se você usar HOST_NAME() em um filtro (e não substituir o valor de HOST_NAME()) não altere o nome do computador no Assinante.  
  
-   Filtros de junção não deveriam conter funções dinâmicas (funções como HOST_NAME() e SUSER_SNAME() que avaliam para um valor diferente dependendo do Assinante que está sincronizando). Somente filtros de linha com parâmetros deveriam conter funções dinâmicas.  
  
-   Não podem ser usadas funções não determinísticas em uma cláusula de filtro. Para obter mais informações sobre funções não determinísticas, consulte [Deterministic and Nondeterministic Functions](../../user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
-   Exibições referenciadas em cláusulas de filtro de junção ou cláusulas de filtro com parâmetros não deveriam conter funções dinâmicas.  
  
-   Não deveria haver nenhuma relação de filtro de junção circular na publicação.  
  
### <a name="database-collation"></a>Ordenação de banco de dados  
  
-   Quando partições pré-computadas são usadas, a ordenação do banco de dados é sempre usada ao fazer comparações, ao invés de ordenação de tabela ou coluna. Considere o cenário a seguir.  
  
    -   Um banco de dados com uma ordenação com diferenciação de maiúsculas e minúsculas contém uma tabela com uma ordenação de diferenciação de maiúsculas e minúsculas.  
  
    -   A tabela contém uma coluna **ComputerName**, que é comparada ao nome do host do Assinante em um filtro com parâmetros.  
  
    -   A tabela contém uma linha com o valor "MYCOMPUTER" e uma linha com o valor "mycomputer" nesta coluna.  
  
     Se o Assinante sincronizar com o nome de host “mycomputer”, o Assinante receberá apenas uma linha, porque a comparação é com diferenciação de maiúsculas e minúsculas (a ordenação do banco de dados). Se partições de pré-computadas não forem usadas, o Assinante receberá ambas as linhas, porque a tabela tem uma ordenação sem diferenciação de maiúsculas e minúsculas.  
  
## <a name="performance-of-precomputed-partitions"></a>Desempenho de partições pré-computadas  
 Há um pequeno custo de desempenho com partições pré-computadas quando as alterações são carregadas do Assinante para o Publicador, mas o tempo de processamento em massa de mesclagem é gasto avaliando as partições e baixando as alterações do Publicador para o Assinante, portanto, o ganho da rede ainda pode ser significativo. O benefício de desempenho irá variar, dependendo do número de Assinantes, sincronizando simultaneamente e o número de atualizações por sincronização que move linhas de uma partição a outra.  
  
## <a name="see-also"></a>Consulte também  
 [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md)  
  
  
