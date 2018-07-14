---
title: Interface do usuário do Designer de Consultas Relacional (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10012"
helpviewer_keywords:
- query designers
- accessing data, query designer
- relational query designer
ms.assetid: cd5fa70c-5218-40d5-9ae6-02d798b5c485
caps.latest.revision: 22
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cbcbb6c64ef5a11db341d1a49c5d966991661a84
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181863"
---
# <a name="relational-query-designer-user-interface-report-builder"></a>Interface de usuário do Designer de Consulta relacional (Construtor de Relatórios)
  Construtor de relatórios fornece um designer de consultas gráficas e um designer de consulta baseado em texto para ajudá-lo a criar uma consulta que especifica os dados para recuperar a partir [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)] bancos de dados relacionais e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] para um conjunto de dados do relatório. Use o designer de consultas gráficas para explorar os metadados, criar uma consulta interativamente e exibir os dados da consulta. Use o designer de consulta baseado em texto para exibir a consulta que foi criada pelo designer de consultas gráficas ou modificar uma consulta. Também é possível importar uma consulta existente de um arquivo ou relatório.  
  
> [!NOTE]  
>  No Construtor de Relatórios, para especificar uma consulta para tipos de fontes de dados Oracle, OLE DB, ODBC e Teradata, você deve usar o designer de consulta baseado em texto. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
> [!IMPORTANT]  
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.  
  
## <a name="graphical-query-designer"></a>Designer de Consultas Gráficas  
 No designer de consultas gráficas, é possível explorar as tabelas e exibições do banco de dados, criar interativamente a instrução SQL SELECT que especifica as tabelas e colunas do banco de dados cujos dados devem ser recuperados para um conjunto de dados. Você escolhe os campos a serem incluídos no conjunto de dados e, opcionalmente, especifica os filtros que limitam os dados desse conjunto. Você pode especificar que os filtros sejam usados como parâmetros e fornecer o valor do filtro em tempo de execução. Se você escolher várias tabelas relacionadas, o designer de consulta descreverá a relação entre conjuntos de duas tabelas.  
  
 O designer de consultas gráficas é dividido em três áreas. Se a consulta usar tabelas/exibições ou procedimentos armazenados/funções com valor de tabela, o layout do designer de consulta será alterado.  
  
> [!NOTE]  
>  O [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] não dá suporte a procedimentos armazenados nem a funções com valor de tabela.  
  
 A figura a seguir mostra o designer de consultas gráficas quando ele é usado com tabelas ou exibições.  
  
 ![Designer gráfico para consultas](../../analysis-services/media/rsqd-relational-graphical.gif "Designer gráfico para consultas")  
  
 A figura a seguir mostra o designer de consultas gráficas quando ele é usado com procedimentos armazenados ou funções com valor de tabela.  
  
 ![Procedimento armazenado no designer de consultas gráficas](../../analysis-services/media/rs-relational-graphical-sp.gif "Procedimento armazenado no designer de consultas gráficas")  
  
 A tabela a seguir descreve a função de cada painel.  
  
 [Exibição de banco de dados](#DatabaseView)  
 Mostra uma exibição hierárquica de tabelas, exibições, procedimentos armazenados e funções com valor de tabela que são organizadas por esquema de banco de dados.  
  
 [Campos selecionados](#SelectedFields)  
 Exibe a lista de nomes de campos de banco de dados dos itens selecionados no painel de exibição Banco de Dados. Esses campos se tornam a coleção de campos do conjunto de dados de relatório.  
  
 [Parâmetros de função](#FunctionParameters)  
 Exibe a lista de parâmetros de entrada para procedimentos armazenados ou funções com valor de tabela no painel de exibição Banco de Dados.  
  
 [Relações](#Relationships)  
 Exibe uma lista de relações inferidas de campos selecionados para tabelas ou exibições no painel Exibição do banco de dados ou as relações criadas manualmente.  
  
 [Filtros aplicados](#AppliedFilters)  
 Exibe uma lista de campos e critérios de filtragem para tabelas ou exibições na exibição Banco de Dados.  
  
 [Resultados da consulta](#QueryResults)  
 Exibe dados de exemplo do conjunto de resultados da consulta gerada automaticamente.  
  
###  <a name="DatabaseView"></a> Painel Exibição de Banco de Dados  
 O painel Exibição de Banco de Dados exibe os metadados de objetos de banco de dados que você tem permissões para exibir, o que é determinado pela conexão da fonte de dados e credenciais. A exibição hierárquica exibe objetos de banco de dados organizados por esquema de banco de dados. Expanda o nó de cada esquema para exibir tabelas, exibições, procedimentos armazenados e funções com valor de tabela. Expanda uma tabela ou exibição para exibir as colunas.  
  
###  <a name="SelectedFields"></a> Painel Campos Selecionados  
 O painel Campos Selecionados exibe os campos do conjunto de dados do relatório e os grupos e agregações a serem incluídos na consulta.  
  
 As seguintes opções são exibidas:  
  
-   **Campos selecionados** Exibe os campos do banco de dados que você seleciona para tabelas ou exibições ou os parâmetros de entrada para procedimentos armazenados ou funções com valor de tabela. Os campos mostrados neste painel se tornam a coleção de campos do conjunto de dados de relatório.  
  
     Use o painel de dados do relatório para exibir o conjunto de campos de um conjunto de dados de relatório. Esses campos representam os dados que você pode exibir em tabelas, gráficos e outros itens de relatório ao exibir um relatório.  
  
-   **Grupo e Agregação** Alterna o uso do agrupamento e das agregações na consulta. Se você desativar o recurso de agrupamento e agregação depois de adicionar o agrupamento e as agregações, eles serão removidos. O texto **(nenhum)** indica que não é usado nenhum agrupamento ou agregação. Se você reativar o recurso de agrupamento e agregação, o agrupamento e as agregações anteriores serão restaurados.  
  
-   **Excluir Campo** Exclui o campo selecionado.  
  
#### <a name="group-and-aggregate"></a>Grupo e Agregação  
 As consultas a bancos de dados com uma tabela grande podem retornar várias linhas de dados que são muito grandes para serem úteis em um relatório e têm um impacto de desempenho na rede que transporta a enorme quantidade de dados e no servidor de relatórios que processa o relatório. Para limitar o número de linhas de dados, a consulta pode incluir agregações de SQL que resumem os dados no servidor de banco de dados. As agregações SQL são diferentes de agregações do lado do cliente, que são aplicadas quando o relatório é renderizado.  
  
 As agregações fornecem resumos de dados, e os dados são agrupados para oferecer suporte à agregação que entrega os dados resumidos. Quando você usa uma agregação na consulta, os outros campos retornados pela consulta são agrupados automaticamente e a consulta inclui a cláusula SQL GROUP BY. É possível resumir dados sem adicionar uma agregação usando somente a opção **Agrupado por** na lista **Grupo e Agregação** . Muitas das agregações incluem uma versão que usa a palavra-chave DISTINCT. A inclusão de DISTINCT elimina valores duplicados.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa [!INCLUDE[tsql](../../../includes/tsql-md.md)] e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] usa [!INCLUDE[DWsql](../../includes/dwsql-md.md)]. Ambos os dialetos da linguagem SQL dão suporte à cláusula, à palavra-chave e às agregações fornecidas pelo designer de consulta.  
  
 Para obter mais informações sobre o [!INCLUDE[tsql](../../../includes/tsql-md.md)], consulte [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference)nos [Manuais Online](http://go.microsoft.com/fwlink/?LinkId=141687) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em msdn.microsoft.com.  
  
 A tabela a seguir lista as agregações e fornece descrições resumidas delas.  
  
|Agregado|Description|  
|---------------|-----------------|  
|Avg|Retorna a média dos valores em um grupo. Implementa a agregação SQL AVG.|  
|Count|Retorna o número de itens de um grupo. Implementa a agregação SQL COUNT.|  
|Count Big|Retorna o número de itens de um grupo. Ela é a agregação SQL COUNT_BIG. A diferença entre COUNT e COUNT_BIG é que COUNT_BIG sempre retorna um valor de tipo de dados `bigint`.|  
|Mín|Retorna o valor mínimo de um grupo. Implementa a agregação SQL MIN.|  
|Max|Retorna o valor máximo em um grupo. Implementa a agregação SQL MAX.|  
|StDev|Retorna o desvio padrão estatístico de todos os valores de um grupo. Implementa a agregação SQL STDEV.|  
|StDevP|Retorna o desvio padrão estatístico para a população de todos os valores da expressão especificada de um grupo. Implementa a agregação SQL STDEVP.|  
|SUM|Retorna a soma de todos os valores do grupo. Implementa a agregação SQL SUM.|  
|Var|Retorna a variação estatística de todos os valores do grupo. Implementa a agregação SQL VAR.|  
|VarP|Retorna a variação estatística para a população de todos os valores do grupo. Implementa a agregação SQL VARP.|  
|Avg Distinct|Retorna médias exclusivas. Implementa uma combinação da agregação AVG e da palavra-chave DISTINCT.|  
|Count Distinct|Retorna contagens exclusivas. Implementa uma combinação da agregação COUNT e da palavra-chave DISTINCT.|  
|Count Big Distinct|Retorna a contagem exclusiva de itens de um grupo. Implementa uma combinação da agregação COUNT_BIG e da palavra-chave DISTINCT.|  
|StDev Distinct|Retorna desvios padrão estatísticos exclusivos. Implementa uma combinação da agregação STDEV e da palavra-chave DISTINCT.|  
|StDevP Distinct|Retorna desvios padrão estatísticos exclusivos. Implementa uma combinação da agregação STDEVP e da palavra-chave DISTINCT.|  
|Sum Distinct|Retorna somas exclusivas. Implementa uma combinação da agregação SUM e da palavra-chave DISTINCT.|  
|Var Distinct|Retorna variações estatísticas exclusivas. Implementa uma combinação da agregação VAR e da palavra-chave DISTINCT.|  
|VarP Distinct|Retorna variações estatísticas exclusivas. Implementa uma combinação da agregação VARP e da palavra-chave DISTINCT.|  
  
###  <a name="FunctionParameters"></a> Painel Parâmetros de Função  
 O painel Parâmetros de Função exibe os parâmetros de um procedimento armazenado ou função com valor de tabela. As seguintes colunas são exibidas:  
  
-   **Nome do Parâmetro** Exibe o nome do parâmetro definido pelo procedimento armazenado ou função com valor de tabela.  
  
-   **Valor** Um valor a ser usado para o parâmetro quando a consulta é executada para recuperar dados a serem exibidos no painel Resultados da Consulta em tempo de design. Esse valor não é usado quando o relatório executado em tempo de execução.  
  
###  <a name="Relationships"></a> Painel Relações  
 O painel Relações exibe as relações de junção. As relações podem ser detectadas automaticamente a partir de relações de chave estrangeira recuperadas dos metadados de banco do dados. Se preferir, você pode criá-las manualmente.  
  
 As seguintes opções são exibidas:  
  
-   **Detecção Automática** Alterna o recurso de detecção automática que cria automaticamente relações entre tabelas. Se a detecção automática estiver ativada, o designer de consulta criará relações a partir de chaves estrangeiras nas tabelas; caso contrário, você deverá criar as relações manualmente. Quando você seleciona tabelas no painel **Exibição do banco de dados** , a detecção automática tenta criar relações automaticamente. Se você ativar a detecção automática depois de criar junções manualmente, essas junções serão descartadas.  
  
    > [!IMPORTANT]  
    >  Ao usar com [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] os metadados necessários à criação de junções não são fornecidos e as relações não podem ser detectadas automaticamente. Se a consulta recuperar dados de [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)], todas as junções da tabela deverão ser criadas manualmente.  
  
-   **Adicionar Relação** Adiciona uma relação à lista de **Relações** .  
  
     Se a detecção automática estiver ativada, as tabelas cujas colunas são usadas na consulta serão adicionadas automaticamente à lista de **Relações** . Quando a detecção automática identifica que há duas tabelas relacionadas, uma tabela é adicionada à coluna **Tabela Esquerda** , a outra à coluna **Tabela Direita** e uma junção interna é criada entre elas. Cada relação gera uma cláusula JOIN na consulta. Se as tabelas não forem relacionadas, todas elas serão listadas na coluna **Tabela Esquerda** e a coluna **Tipo de Junção** indicará que as tabelas não estão relacionadas a outras tabelas. Quando a detecção automática estiver ativada, não será possível adicionar relações manualmente entre tabelas que a detecção automática considerar não relacionadas.  
  
     Se a detecção automática estiver desativada, será possível adicionar e alterar relações entre tabelas. Clique em **Editar Campos** para especificar os campos a serem usados para unir as duas tabelas.  
  
     A ordem na qual as relações são exibidas na lista de **Relações** é a ordem na qual as junções serão executadas na consulta. É possível alterar a ordem das relações movendo-as para cima e para baixo na lista.  
  
     Ao usar várias relações em uma consulta, uma das tabelas em cada relação, exceto a primeira, deve ser referenciada em relações futuras.  
  
     Se ambas as tabelas em uma relação forem referenciadas por uma relação anterior, a relação não irá gerar uma cláusula de junção à parte; em vez disso, uma condição de junção é adicionada à cláusula de junção gerada para a relação anterior. O tipo de junção é inferido pela relação anterior que referenciou as mesmas tabelas.  
  
-   **Editar Campos** Abre a caixa de diálogo **Editar Campos Relacionados** na qual você adiciona e modifica relações entre tabelas. Você escolheu os campos nas tabelas direita e esquerda a serem unidos. É possível unir vários campos da tabela esquerda e da tabela direita para especificar várias condições de junção em uma relação. Os dois campos que unem as tabelas esquerda e direita não precisam ter o mesmo nome. Os campos unidos devem ter tipos de dados compatíveis.  
  
-   **Excluir Relação**  Exclui a relação selecionada **.**  
  
-   **Mover para Cima** e **Mover para Baixo** Move relações para cima ou para baixo na lista de **Relações** . A sequência na qual as relações são colocadas na consulta pode afetar os resultados da consulta. As relações são adicionadas à consulta na ordem em que são exibidas na lista de **Relações** .  
  
 As seguintes colunas são exibidas:  
  
-   **Tabela Esquerda** Exibe o nome da primeira tabela que faz parte de uma relação de junção.  
  
-   **Tipo de Junção** Exibe o tipo de instrução SQL JOIN usada na consulta gerada automaticamente. Por padrão, se uma restrição de chave estrangeira for detectada, INNER JOIN será usada. Outros tipos de junção podem ser LEFT JOIN ou RIGHT JOIN. Se nenhum desses tipos de junção se aplicar, a coluna **Tipo de Junção** exibirá **Não relacionado**. Nenhuma junção CROSS JOIN é criada para tabelas não relacionadas. Em vez disso, você deve criar relações manualmente unindo colunas nas tabelas esquerda e direita. Para obter mais informações sobre tipos de JOINs, consulte "Fundamentos de JOIN" nos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [Manuais Online do](http://go.microsoft.com/fwlink/?LinkId=141687) em msdn.microsoft.com...  
  
-   **Tabela Direita** Exibe o nome da segunda tabela na relação de junção.  
  
-   **Campos de Junção** Lista os pares de campos unidos. Se uma relação tiver várias condições de junção, os pares de campos unidos serão separados por vírgulas (,).  
  
###  <a name="AppliedFilters"></a> Painel Filtros Aplicados  
 O painel Filtros Aplicados exibe os critérios usados para limitar o número de linhas de dados recuperadas no tempo de execução. Os critérios especificados nesse painel são usados para gerar uma cláusula SQL WHERE. Quando você seleciona a opção de parâmetro, um parâmetro de relatório é criado automaticamente. Os parâmetros de relatório se baseiam em parâmetros de consulta que permitem a um usuário especificar valores para a consulta, para controlar os dados no relatório.  
  
 As seguintes colunas são exibidas:  
  
-   **Nome do Campo** Exibe o nome do campo ao qual aplicar os critérios.  
  
-   **Operador** Exibe a operação a ser usada na expressão de filtro.  
  
-   **Valor** Exibe o valor a ser usado na expressão de filtro.  
  
-   **Parâmetro** Exibe a opção para adicionar um parâmetro à consulta. Use as propriedades do conjunto de dados para exibir as relações entre o parâmetro de consulta e o parâmetro do relatório.  
  
###  <a name="QueryResults"></a> Painel Resultados da Consulta  
 O painel Resultados da Consulta exibe os resultados para a consulta automaticamente gerada que é especificada por seleções nos outros painéis. As colunas do conjunto de resultados são os campos que você especifica no painel Campos Selecionados e os dados de linha são limitados pelos filtros que você especifica no painel Filtros Aplicados. Se a consulta incluir agregações, o conjunto de resultados incluirá as novas colunas de agregações. Por exemplo, se a **Cor** da coluna for agregada com a agregação Count, os resultados da consulta incluirão uma nova coluna. Por padrão, essa coluna é denominada **Count_Color**.  
  
 Esses dados representam valores da fonte de dados no momento em que você executa a consulta. Os dados não são salvos na definição de relatório. Os dados reais do relatório são recuperados quando o relatório é processado.  
  
 A ordem de classificação do conjunto de resultados é determinada pela ordem em que os dados são recuperados da fonte de dados. A ordem de classificação pode ser alterada modificando-se a consulta ou após a recuperação dos dados para o relatório.  
  
### <a name="graphical-query-designer-toolbar"></a>Barra de ferramentas do designer de consultas gráficas  
 A barra de ferramentas do designer de consulta relacional fornece os seguintes botões para ajudá-lo a especificar ou exibir os resultados de uma consulta.  
  
|Botão|Description|  
|------------|-----------------|  
|**Editar como Texto**|Alterna para o designer de consulta baseado em texto para exibir a consulta gerada automaticamente ou para modificar a consulta.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Há suporte para os tipos de arquivo .sql e .rdl.|  
|**Executar consulta**|Executa a consulta. O painel Resultados da consulta exibe o conjunto de resultados.|  
  
## <a name="understanding-automatically-generated-queries"></a>Entendendo consultas geradas automaticamente  
 Quando você seleciona tabelas e colunas ou procedimentos armazenados e exibições no painel Exibição de Banco de dados, o designer de consulta recupera a chave primária subjacente e relações de chave estrangeira do esquema de banco de dados. Ao analisar essas relações, o designer de consulta detecta as relações entre duas tabelas e adiciona junções à consulta. Dessa forma, é possível modificar a consulta adicionando grupos e agregações, adicionando ou alterando relações e adicionando filtros. Para exibir o texto da consulta que mostra as colunas das quais os dados são recuperados, as junções entre tabelas e qualquer grupo ou agregação, clique em **Editar Como Texto**.  
  
## <a name="text-based-query-designer"></a>Designer de Consulta com Base em Texto  
 Para ter o máximo controle sobre sua consulta, use o designer de consulta baseado em texto. Para mudar para o designer de consulta baseado em texto, na barra de ferramentas, clique em **Editar como Texto**. Depois que você editar uma consulta no designer de consulta baseado em texto, não poderá mais usar o designer de consulta relacional. A consulta sempre será aberta no designer de consulta baseado em texto. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Consulte também  
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md)  
  
  
