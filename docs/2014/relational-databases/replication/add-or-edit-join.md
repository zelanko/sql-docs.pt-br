---
title: Adicionar ou editar junção | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.addeditjoin.f1
ms.assetid: 3b546560-720f-48b8-9d63-cf159290e9d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abe1fb743410bdf7e0e9b586fc175a4308d8e8ef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130328"
---
# <a name="add-or-edit-join"></a>Adicionar ou Editar Junção
  As caixas de diálogo **Adicionar Junção** e **Editar Junção** permitem adicionar e editar filtros de junção para publicações de mesclagem.  
  
> [!NOTE]  
>  Editar um filtro em uma publicação existente requer um novo instantâneo para a publicação. Se uma publicação tiver assinaturas, as assinaturas deverão ser reiniciadas. Para obter mais informações sobre alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](publish/change-publication-and-article-properties.md).  
  
 Um filtro de junção permite que uma tabela seja filtrada com base na forma pela qual uma tabela relacionada é filtrada na publicação. Geralmente uma tabela pai é filtrada usando um filtro de linha com parâmetros; depois um ou mais filtros de junção são definidos quase da mesma forma pela qual as junções são definidas entre tabelas. Os filtros de junção estendem os filtros da linha para que os dados nas tabelas relacionadas sejam replicados somente se corresponderem à cláusula do filtro de junção.  
  
 Os filtros de junção geralmente seguem as relações chave primária/chave estrangeira definidas para as tabelas nas quais são aplicados, mas não estão estritamente limitados a essas relações. O filtro de junção pode se basear em qualquer lógica que compara dados relacionados em duas tabelas de artigo.  
  
> [!IMPORTANT]  
>  Os filtros de junção podem envolver um número ilimitado de tabelas, mas filtros com um grande número de tabelas podem impactar o desempenho durante o processo de mesclagem. Se você estiver gerando filtros de junção de cinco ou mais tabelas, considere outras soluções: não filtre tabelas pequenas, que não estão sujeitas a alterações ou que sejam basicamente tabelas de pesquisa. Use filtros de junção somente entre tabelas que devem ser particionadas entre Assinantes.  
  
## <a name="options"></a>Opções  
 Essa caixa de diálogo envolve um processo de três etapas para criar um filtro de junção entre duas tabelas. A criação de mais de um filtro de junção requer mais de uma passagem pela caixa de diálogo.  
  
1.  **Verifique a tabela filtrada e selecione a tabela unida**  
  
    -   Se você estiver adicionando uma nova junção, verifique se a tabela na caixa de texto **Tabela Filtrada** está correta (se não estiver correta, clique em **Cancelar**, selecione a tabela correta na página **Filtrar Linhas da Tabela** e clique em **Adicionar Junção** para retornar à caixa de diálogo). Depois selecione uma tabela na caixa de listagem suspensa **Tabela Unida** .  
  
    -   Se você estiver editando uma junção existente, os nomes de tabela serão especificados e não poderão ser alterados. Para alterar as tabelas envolvidas na junção, é necessário alterar o filtro da tabela existente na página **Filtrar Linhas da Tabela** e criar uma nova junção entre tabelas diferentes.  
  
2.  **Crie a instrução de junção**  
  
    -   Se você estiver adicionando uma nova junção, selecione **Usar o construtor para criar a instrução** ou **Gravar a instrução de junção manualmente**. Se você começar a gravar a junção manualmente, não poderá usar o construtor.  
  
         Se você selecionar para usar o construtor, use as colunas na grade (**Conjunção**, **Coluna da Tabela Filtrada**, **Operador**e **Coluna da Tabela Unida**) para criar uma instrução de junção. Cada coluna na grade contém uma caixa de listagem suspensa, permitindo que você selecione duas colunas e um operador (**=**, **<>**, **<=**, **\<**, **>=**, **>**, **like**). Os resultados são exibidos na área de texto **Visualizar** . Se a junção envolver mais de um par de colunas, selecione uma conjunção (**AND** ou **OR**) na coluna **Conjunção** e insira mais duas colunas e outro operador.  
  
         Se você selecionar para gravar a instrução manualmente, grave a instrução de junção na área de texto **Instrução de Junção** . Use a caixa de listagem **Colunas da Tabela Filtrada** e **Colunas da Tabela Unida** para arrastar e soltar colunas na área de texto **Instrução de Junção** .  
  
    -   Se você estiver editando uma junção existente, deverá fazer as edições manualmente.  
  
3.  **Especificar Opções de Junção**  
  
    -   Se a coluna em que você une a tabela filtrada for exclusiva, selecione **Chave Exclusiva**. O processo de mesclagem terá otimizações de desempenho especiais disponíveis se a coluna for exclusiva.  
  
        > [!CAUTION]  
        >  A seleção dessa opção indica que a relação entre tabelas pai e filho em um filtro de junção é de um para um ou um para muitos. Só selecione essa opção se você tiver uma restrição na coluna de junção na tabela pai que garanta a exclusividade. Se a opção for definida incorretamente, poderá ocorrer não convergência de dados.  
  
    -   Somente[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Por padrão, os processos de replicação de mesclagem são alterados em uma base de linha por linha durante a sincronização. Para que as alterações relacionadas sejam processadas como uma unidade, selecione **Registro Lógico**. Essa opção só estará disponível se os requisitos de  artigo e publicação para uso de registros lógicos forem atendidos. Para obter mais informações, consulte a seção "Considerações para uso de registros lógicos" em [Agrupar alterações a linhas relacionadas com registros lógicos](merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Depois de adicionar ou editar um filtro, clique em **OK** para salvar as alterações e fechar a caixa de diálogo. O filtro que você especificou é analisado e executado na tabela, na cláusula SELECT. Se a instrução de filtro contiver erros de sintaxe ou outros problemas, você será notificado e poderá editar a instrução do filtro.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Filtrar os dados publicados](publish/filter-published-data.md)   
 [Join Filters](merge/join-filters.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)  
  
  
