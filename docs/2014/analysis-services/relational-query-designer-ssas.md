---
title: Designer de consulta relacional (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.relquerydesginer.f1
ms.assetid: 9399b1d1-1ad2-44df-bd11-bef60fbf01ec
author: minewiskan
ms.author: owend
ms.openlocfilehash: 79765f589dcc649bdb2d12bd9dda0d4c955ae916
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883926"
---
# <a name="relational-query-designer-ssas"></a>Designer de consulta relacional (SSAS)
  O designer de consulta relacional ajuda a criar uma consulta que especifica os dados a serem recuperados e os bancos de dados [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] relacionais e [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] . Use o designer de consultas gráficas para explorar os metadados, criar a consulta interativamente e exibir os dados da consulta.  Use o designer de consulta baseado em texto para exibir a consulta que foi criada pelo designer de consultas gráficas ou modificar uma consulta. Também é possível importar uma consulta existente de um arquivo ou relatório.  
  
 Se você preferir, será possível escrever a consulta na linguagem SQL usando o editor baseado em texto. Para mudar para o designer de consulta baseado em texto, na barra de ferramentas, clique em **Editar como Texto**. Depois de editar uma consulta no designer de consulta baseado em texto, você não poderá mais usar o designer de consultas gráficas.  
  
> [!NOTE]  
>  Para especificar uma consulta para tipos de fontes de dados Oracle, OLE DB, ODBC e Teradata, é necessário usar o designer de consulta baseado em texto.  
  
> [!IMPORTANT]  
>  Os usuários acessam fontes de dados quando criam e executam consultas. Você deve conceder permissões mínimas nas fontes de dados, como permissões somente leitura.  
>   
>  As credenciais do usuário atual, e não as credenciais especificadas na página Informações sobre Representação, são usadas na conexão à fonte de dados quando uma consulta é executada.  
  
## <a name="graphical-query-designer"></a>Designer de Consultas Gráficas  
 No designer de consultas gráficas, é possível explorar as tabelas e exibições do banco de dados, criar interativamente a instrução SQL SELECT que especifica as tabelas e colunas do banco de dados cujos dados devem ser recuperados para um conjunto de dados. Você escolhe os campos a serem incluídos no conjunto de dados e, opcionalmente, especifica os filtros que limitam os dados desse conjunto. Você pode especificar que os filtros sejam usados como parâmetros e fornecer o valor do filtro em tempo de execução. Se você escolher várias tabelas, o designer de consulta descreverá a relação entre conjuntos de duas tabelas.  
  
 O designer de consultas gráficas é dividido em três áreas. Dependendo de a consulta usar tabelas/exibições ou procedimentos armazenados/funções com valor de tabela, o layout do designer de consulta é alterado.  
  
> [!NOTE]  
>  O [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] não dá suporte a procedimentos armazenados nem a funções com valor de tabela.  
  
 A figura a seguir mostra o designer de consultas gráficas quando ele é usado com tabelas ou exibições.  
  
 ![Designer de consultas gráficas](media/rsqd-relational-graphical.gif "Designer de consultas gráficas")  
  
 A figura a seguir mostra o designer de consultas gráficas quando ele é usado com procedimentos armazenados ou funções com valor de tabela.  
  
 ![Procedimento armazenado no designer de consultas gráficas](media/rs-relational-graphical-sp.gif "Procedimento armazenado no designer de consultas gráficas")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|[Exibição de banco de dados](#DatabaseView)|Mostra uma exibição hierárquica de tabelas, exibições, procedimentos armazenados e funções com valor de tabela que são organizadas por esquema de banco de dados.|  
|[Campos selecionados](#SelectedFields)|Exibe a lista de nomes de campos de banco de dados dos itens selecionados no painel de exibição Banco de Dados. Esses campos se tornam a coleção de campos para o conjunto de dados.|  
|[Parâmetros de função](#FunctionParameters)|Exibe a lista de parâmetros de entrada para procedimentos armazenados ou funções com valor de tabela no painel de exibição Banco de Dados.|  
|[Relacionamentos](#Relationships)|Exibe uma lista de relações inferidas de campos selecionados para tabelas ou exibições no painel Exibição do banco de dados ou as relações criadas manualmente.|  
|[Filtros aplicados](#AppliedFilters)|Exibe uma lista de campos e critérios de filtragem para tabelas ou exibições na exibição Banco de Dados.|  
|[Resultados da consulta](#QueryResults)|Exibe dados de exemplo do conjunto de resultados da consulta gerada automaticamente.|  
  
###  <a name="database-view-pane"></a><a name="DatabaseView"></a> Painel Exibição de Banco de Dados  
 O painel Exibição de Banco de Dados exibe os metadados de objetos de banco de dados que você tem permissões para exibir, o que é determinado pela conexão da fonte de dados e credenciais. A exibição hierárquica exibe objetos de banco de dados organizados por esquema de banco de dados. Expanda o nó de cada esquema para exibir tabelas, exibições, procedimentos armazenados e funções com valor de tabela. Expanda uma tabela ou exibição para exibir as colunas.  
  
###  <a name="selected-fields-pane"></a><a name="SelectedFields"></a>Painel campos selecionados  
 O painel Campos Selecionados exibe os campos do conjunto de dados e os grupos e agregações a serem incluídos na consulta.  
  
 As seguintes opções são exibidas:  
  
-   **Campos selecionados** Exibe os campos do banco de dados que você seleciona para tabelas ou exibições ou os parâmetros de entrada para procedimentos armazenados ou funções com valor de tabela. Os campos exibidos neste painel se tornam a coleção de campos do conjunto de dados.  
  
     Use o painel de dados do relatório para exibir o conjunto de campos de um conjunto de dados.  
  
-   **Grupo e Agregação** Alterna o uso do agrupamento e das agregações na consulta. Se você desativar o recurso de agrupamento e agregação depois de adicionar o agrupamento e as agregações, eles serão removidos. O texto **(nenhum)** indica que não é usado nenhum agrupamento ou agregação. Se você reativar o recurso de agrupamento e agregação, o agrupamento e as agregações anteriores serão restaurados.  
  
-   **Excluir Campo** Exclui o campo selecionado.  
  
#### <a name="group-and-aggregate"></a>Grupo e Agregação  
 As consultas a bancos de dados com uma tabela grande podem retornar várias linhas de dados que são muito grandes para serem úteis e têm um impacto sobre o desempenho da rede que transporta a enorme quantidade de dados. Para limitar o número de linhas de dados, a consulta pode incluir agregações de SQL que resumem os dados no servidor de banco de dados.  
  
 As agregações fornecem resumos de dados, e os dados são agrupados para oferecer suporte à agregação que entrega os dados resumidos. Quando você usa uma agregação na consulta, os outros campos retornados pela consulta são agrupados automaticamente e a consulta inclui a cláusula SQL GROUP BY. É possível resumir dados sem adicionar uma agregação usando somente a opção **Agrupado por** na lista **Grupo e Agregação** . Muitas das agregações incluem uma versão que usa a palavra-chave DISTINCT. A inclusão de DISTINCT elimina valores duplicados.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]usa [!INCLUDE[tsql](../includes/tsql-md.md)] e [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] usa [!INCLUDE[DWsql](../includes/dwsql-md.md)] . Ambos os dialetos da linguagem SQL dão suporte à cláusula, à palavra-chave e às agregações fornecidas pelo designer de consulta.  
  
 Para obter mais informações sobre o [!INCLUDE[tsql](../includes/tsql-md.md)], consulte [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference)nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Manuais Online](https://go.microsoft.com/fwlink/?LinkId=141687) do  em msdn.microsoft.com.  
  
 A tabela a seguir lista as agregações e fornece descrições resumidas delas.  
  
|Agregado|Descrição|  
|---------------|-----------------|  
|Avg|Retorna a média dos valores em um grupo. Implementa a agregação SQL AVG.|  
|Contagem|Retorna o número de itens de um grupo. Implementa a agregação SQL COUNT.|  
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
  
###  <a name="function-parameters-pane"></a><a name="FunctionParameters"></a> Painel Parâmetros de Função  
 O painel Parâmetros de Função exibe os parâmetros de um procedimento armazenado ou função com valor de tabela. As seguintes colunas são exibidas:  
  
-   **Nome do Parâmetro** Exibe o nome do parâmetro definido pelo procedimento armazenado ou função com valor de tabela.  
  
-   **Valor** Um valor a ser usado para o parâmetro quando a consulta é executada para recuperar dados a serem exibidos no painel Resultados da Consulta em tempo de design. Este valor não é usado em tempo de execução.  
  
###  <a name="relationships-pane"></a><a name="Relationships"></a>Painel relações  
 O painel Relações exibe as relações de junção. As relações podem ser detectadas automaticamente a partir de relações de chave estrangeira recuperadas dos metadados de banco do dados. Se preferir, você pode criá-las manualmente.  
  
 As seguintes opções são exibidas:  
  
-   **Detecção Automática** Alterna o recurso de detecção automática que cria automaticamente relações entre tabelas. Se a detecção automática estiver ativada, o designer de consulta criará relações a partir de chaves estrangeiras nas tabelas; caso contrário, você deverá criar as relações manualmente. Quando você seleciona tabelas no painel **Exibição do banco de dados** , a detecção automática tenta criar relações automaticamente. Se você ativar a detecção automática depois de criar junções manualmente, essas junções serão descartadas.  
  
    > [!IMPORTANT]  
    >  Durante o uso com [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] , os metadados necessários à criação de junções não são fornecidos e as relações não podem ser detectadas automaticamente. Se a consulta recuperar dados de [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)], todas as junções da tabela deverão ser criadas manualmente.  
  
-   **Adicionar Relação** Adiciona uma relação à lista de **Relações** .  
  
     Se a detecção automática estiver ativada, as tabelas cujas colunas são usadas na consulta serão adicionadas automaticamente à lista de **Relações** . Quando a detecção automática identifica que há duas tabelas relacionadas, uma tabela é adicionada à coluna **Tabela Esquerda** , a outra à coluna **Tabela Direita** e uma junção interna é criada entre elas. Cada relação gera uma cláusula JOIN na consulta. Se as tabelas não forem relacionadas, todas elas serão listadas na coluna **Tabela Esquerda** e a coluna **Tipo de Junção** indicará que as tabelas não estão relacionadas a outras tabelas. Quando a detecção automática estiver ativada, não será possível adicionar relações manualmente entre tabelas que a detecção automática considerar não relacionadas.  
  
     Se a detecção automática estiver desativada, será possível adicionar e alterar relações entre tabelas. Clique em **Editar Campos** para especificar os campos a serem usados para unir as duas tabelas.  
  
     A ordem na qual as relações são exibidas na lista de **Relações** é a ordem na qual as junções serão executadas na consulta. É possível alterar a ordem das relações movendo-as para cima e para baixo na lista.  
  
     Ao usar várias relações em uma consulta, uma das tabelas em cada relação, exceto a primeira, deve ser referenciada em relações futuras.  
  
     Se ambas as tabelas em uma relação forem referenciadas por uma relação anterior, a relação não irá gerar uma cláusula de junção à parte; em vez disso, uma condição de junção é adicionada à cláusula de junção gerada para a relação anterior. O tipo de junção é inferido pela relação anterior que referenciou as mesmas tabelas.  
  
-   **Editar Campos** Abre a caixa de diálogo **Editar Campos Relacionados** na qual você adiciona e modifica relações entre tabelas. Você escolheu os campos nas tabelas direita e esquerda a serem unidos. É possível unir vários campos da tabela esquerda e da tabela direita para especificar várias condições de junção em uma relação. Os dois campos que unem as tabelas esquerda e direita não precisam ter o mesmo nome. O tipo de dados dos campos unidos deve ter tipos de dados compatíveis.  
  
-   **Excluir Relação**  Exclui a relação selecionada **.**  
  
-   **Mover para Cima** e **Mover para Baixo** Move relações para cima ou para baixo na lista de **Relações** . A sequência na qual as relações são colocadas na consulta pode afetar os resultados da consulta. As relações são adicionadas à consulta na ordem em que são exibidas na lista de **Relações** .  
  
 As seguintes colunas são exibidas:  
  
-   **Tabela Esquerda** Exibe o nome da primeira tabela que faz parte de uma relação de junção.  
  
-   **Tipo de Junção** Exibe o tipo de instrução SQL JOIN usada na consulta gerada automaticamente. Por padrão, se uma restrição de chave estrangeira for detectada, INNER JOIN será usada. Outros tipos de junção podem ser LEFT JOIN ou RIGHT JOIN. Se nenhum desses tipos de junção se aplicar, a coluna **Tipo de Junção** exibirá **Não relacionado**. Nenhuma junção CROSS JOIN é criada para tabelas não relacionadas. Em vez disso, você deve criar relações manualmente unindo colunas nas tabelas esquerda e direita. Para obter mais informações sobre tipos de JOINs, consulte "Fundamentos de JOIN" nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?LinkId=141687) on msdn.microsoft.com.  
  
-   **Tabela Direita** Exibe o nome da segunda tabela na relação de junção.  
  
-   **Campos de Junção** Lista os pares de campos unidos. Se uma relação tiver várias condições de junção, os pares de campos unidos serão separados por vírgulas (,).  
  
###  <a name="applied-filters-pane"></a><a name="AppliedFilters"></a> Painel Filtros Aplicados  
 O painel Filtros Aplicados exibe os critérios usados para limitar o número de linhas de dados recuperadas no tempo de execução. Os critérios especificados nesse painel são usados para gerar uma cláusula SQL WHERE. Quando você seleciona a opção de parâmetro, um parâmetro é criado automaticamente.  
  
 As seguintes colunas são exibidas:  
  
-   **Nome do Campo** Exibe o nome do campo ao qual aplicar os critérios.  
  
-   **Operador** Exibe a operação a ser usada na expressão de filtro.  
  
-   **Valor** Exibe o valor a ser usado na expressão de filtro.  
  
-   **Parâmetro** Exibe a opção para adicionar um parâmetro à consulta.  
  
###  <a name="query-results-pane"></a><a name="QueryResults"></a> Painel Resultados da Consulta  
 O painel Resultados da Consulta exibe os resultados para a consulta automaticamente gerada que é especificada por seleções nos outros painéis. As colunas do conjunto de resultados são os campos que você especifica no painel Campos Selecionados e os dados de linha são limitados pelos filtros que você especifica no painel Filtros Aplicados.  
  
 Esses dados representam valores da fonte de dados no momento em que você executa a consulta.  
  
 A ordem de classificação do conjunto de resultados é determinada pela ordem em que os dados são recuperados da fonte de dados. A ordem de classificação pode ser alterada com a modificação direta do texto da consulta. Para obter mais informações sobre como usar a cláusula GROUP BY em uma consulta, consulte "GROUP BY (Transact-SQL)" nos [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
### <a name="graphical-query-designer-toolbar"></a>Barra de ferramentas do designer de consultas gráficas  
 A barra de ferramentas do designer de consultas gráficas fornece os botões a seguir para ajudá-lo a especificar ou exibir os resultados de uma consulta.  
  
|Botão|Descrição|  
|------------|-----------------|  
|**Editar como Texto**|Alterna para o designer de consulta baseado em texto para exibir a consulta gerada automaticamente ou para modificar a consulta.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Há suporte para os tipos de arquivo .sql e .rdl.|  
|**Executar consulta**|Executa a consulta. O painel Resultados da consulta exibe o conjunto de resultados.|  
  
## <a name="understanding-automatically-generated-queries"></a>Entendendo consultas geradas automaticamente  
 Quando você seleciona tabelas e colunas ou procedimentos armazenados e exibições no painel Exibição de Banco de dados, o designer de consulta recupera a chave primária subjacente e relações de chave estrangeira do esquema de banco de dados. Ao analisar essas relações, o designer de consulta detecta as relações entre duas tabelas e adiciona junções à consulta. Dessa forma, é possível modificar a consulta adicionando grupos e agregações, adicionando ou alterando relações e adicionando filtros. Para exibir o texto da consulta que mostra as colunas das quais os dados são recuperados, as junções entre tabelas e qualquer grupo ou agregação, clique em **Editar Como Texto**.  
  
## <a name="text-based-query-designer"></a>Designer de Consulta baseado em texto  
 O designer de consulta baseado em texto fornece uma maneira de especificar uma consulta usando a linguagem de consulta com suporte da fonte de dados, executar a consulta e exibir os resultados em tempo de design. É possível especificar várias instruções SQL, consulta ou sintaxe de comando para extensões de processamento de dados e consultas especificadas como expressões.  
  
 Como o designer de consulta baseado em texto não pré-processa a consulta, ele pode acomodar qualquer tipo de sintaxe de consulta. Ele é a ferramenta de designer de consulta padrão para muitos tipos de fonte de dados.  
  
 O designer de consulta baseado em texto exibe uma barra de ferramentas e os dois painéis a seguir:  
  
-   **Consulta** Mostra o texto da consulta, o nome da tabela ou o nome do procedimento armazenado, dependendo do tipo de consulta. Nem todos os tipos de consulta estão disponíveis para todos os tipos de fontes de dados. Por exemplo, nome da tabela tem suporte apenas para o tipo de fonte de dados OLE DB.  
  
-   **Resultado** Mostra os resultados da execução da consulta em tempo de design.  
  
### <a name="text-based-query-designer-toolbar"></a>Barra de ferramentas do Designer de Consulta baseado em texto  
 O designer de consulta baseado em texto fornece uma única barra de ferramentas para todos os tipos de comando. A tabela a seguir lista cada botão da barra de ferramentas e suas respectivas funções.  
  
|Botão|Descrição|  
|------------|-----------------|  
|**Editar como Texto**|Alterna entre o designer de consulta baseado em texto e o designer de consultas gráficas. Nem todos os tipos de fonte de dados dão suporte aos designers de consultas gráficas.|  
|**Importar**|Importa uma consulta existente de um arquivo ou relatório. Apenas os tipos de arquivo .sql e .rdl têm suporte.|  
|![Executar a consulta](media/rsqdicon-run.gif "Executar a consulta")|Executa a consulta e exibe o conjunto de resultados no painel Resultado.|  
|**Tipo de Comando**|Selecione **Text**, **StoredProcedure**ou **TableDirect**. Se um procedimento armazenado tiver parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta quando você clicar em **Executar** na barra de ferramentas e os valores poderão ser preenchidos conforme necessário.<br /><br /> Observe que, se um procedimento armazenado retornar mais de um conjunto de resultados, somente o primeiro conjunto de resultados será usado para popular o conjunto de informações. Observe também que <br />                      **TableDirect** está disponível somente para o tipo de fonte de dados OLE DB.|  
  
#### <a name="command-type-text"></a>Tipo de comando Text  
 Quando você cria um conjunto de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o designer de consulta relacional é aberto por padrão. Para mudar para o designer de consulta baseado em texto, clique no botão de alternância **Editar como Texto** na barra de ferramentas. O designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. A imagem a seguir define cada painel.  
  
 ![Designer de consultas genérico para consulta de dados relacionais](media/rsqd-dsaw-sql-generic.gif "Designer de consultas genérico para consulta de dados relacionais")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Consulta|Exibe o texto da consulta SQL. Use este painel para gravar ou editar uma consulta SQL.|  
|Result|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar**ou clique no botão **Executar** na barra de ferramentas.|  
  
#### <a name="example"></a>Exemplo  
 A consulta a seguir retorna a lista de nomes de uma tabela chamada `ContactType`.  
  
```sql  
SELECT Name FROM ContactType  
```  
  
 Quando você clica em **Executar** na barra de ferramentas, o comando no painel **Consulta** é executado e o resultado, uma lista de nomes, é exibido no painel **Resultado** .  
  
#### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure  
 Quando você seleciona o **Comando typeStoredProcedure**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Insira o nome do procedimento armazenado no painel Consulta e clique em **Executar** na barra de ferramentas. Se o procedimento armazenado usar parâmetros, a caixa de diálogo **Definir Parâmetros de Consulta** será aberta. Insira os valores dos parâmetros do procedimento armazenado.  
  
 A figura a seguir mostra os painéis Consulta e Resultados quando você executa um procedimento armazenado. Neste caso, os parâmetros de entrada são constantes.  
  
 ![Procedimento armazenado no designer de consultas baseadas em texto](media/rs-relational-text-sp.gif "Procedimento armazenado no designer de consultas baseadas em texto")  
  
 A tabela a seguir descreve a função de cada painel.  
  
|Painel|Função|  
|----------|--------------|  
|Consulta|Exibe o nome do procedimento armazenado e os parâmetros de entrada.|  
|Result|Exibe os resultados da consulta. Para executar a consulta, clique com o botão direito do mouse em qualquer painel e clique em **Executar**ou clique no botão **Executar** na barra de ferramentas.|  
  
#### <a name="example"></a>Exemplo  
 A consulta a seguir chama um procedimento armazenado chamado `uspGetWhereUsedProductID`. Quando o procedimento armazenado tiver parâmetros de entrada será necessário fornecer valores de parâmetros ao executar a consulta.  
  
```sql  
uspGetWhereUsedProductID  
```  
  
 Clique no botão **Executar** (**!**). A tabela a seguir fornece um exemplo de `uspGetWhereUsedProductID` parâmetros para os quais você fornece valores na caixa de diálogo **definir parâmetro de consulta** .  
  
|||  
|-|-|  
|*\@StartProductID*|820|  
|*\@CheckDate*|20010115|  
  
#### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect  
 Quando você seleciona o **Comando typeTableDirect**, o designer de consulta baseado em texto apresenta dois painéis: Consulta e Resultado. Se você inserir uma tabela e clicar no botão **Executar** , todas as colunas dessa tabela serão retornadas.  
  
#### <a name="example"></a>Exemplo  
 Para um tipo de fonte de dados OLE DB, a consulta de banco de dados a seguir retorna um conjunto de resultados para todos os tipos de contato da tabela `ContactType`.  
  
 `ContactType`  
  
 Quando você insere o nome da tabela `ContactType`, isso equivale a criar a instrução SQL `SELECT * FROM ContactType`.  
  
  
