---
title: O que &#39; s New in Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
caps.latest.revision: 97
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 212fbb3618bbccc58ea077d59f15dca3c31ca71f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-analysis-services"></a>O que &#39; s no Analysis Services
SQL Server 2016 Analysis Services inclui vários novos aprimoramentos fornecer melhor desempenho, criação de solução mais fácil, gerenciamento de banco de dados automatizada, relações aprimoradas com bidirecional entre a filtragem, paralelo processamento da partição, e muito mais. O cerne da maioria dos aprimoramentos para esta versão é o novo nível de compatibilidade 1200 para bancos de dados de modelo tabular.     

## <a name="azure-analysis-services"></a>Azure Analysis Services
Anunciado na conferência 2016 SQL PASSA, o Analysis Services agora está disponível na nuvem como um serviço do Azure. **Serviços de análise do Azure** dá suporte a modelos de tabela nos níveis de compatibilidade 1200 e superior. DirectQuery, partições, segurança de nível de linha, relações bidirecionais e traduções todas têm suporte. Para saber mais e experimentar gratuitamente, consulte [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/). 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>Novidades no SQL Server 2016 Service Pack 1 (SP1) Analysis Services

[Baixe o SQL Server 2016 SP1](http://www.microsoft.com/download/details.aspx?id=54276) 

O SQL Server 2016 Service SP1 Analysis Services oferece melhor desempenho e escalabilidade por meio de reconhecimento NUMA (acesso não uniforme a memória) e otimização de alocação de memória com base no **Intel Threading Building Blocks** (Intel TBB). Essa nova funcionalidade ajuda a reduzir o custo total de propriedade (TCO), oferecendo suporte a mais usuários em servidores corporativos em menor quantidade e mais potentes. 

Em particular, o SQL Server 2016 SP1 Analysis Services apresenta melhorias nas principais áreas a seguir:

-   **Reconhecimento NUMA** – para o melhor suporte ao NUMA, o mecanismo na memória (VertiPaq) no Analysis Services agora mantém uma fila de trabalho separada em cada nó NUMA. Isso garante que os trabalhos de verificação de segmento sejam executados no mesmo nó no qual a memória é alocada para os dados do segmento. Observe que o reconhecimento NUMA é habilitado por padrão somente nos sistemas com, pelo menos, quatro nós NUMA. Em sistemas de dois nós, os custos de acesso à memória alocada remota geralmente não justificam a despesa de gerenciamento específicas de NUMA.
-   **Alocação de memória** – o Analysis Services foi acelerado com o Intel Threading Building Blocks, um alocador escalonável que fornece pools de memória separados para cada núcleo. À medida que aumenta o número de núcleos, o sistema pode ser dimensionado de forma quase linear.
-   **Fragmentação de heap** – o alocador escalonável com base no Intel TBB também ajuda a reduzir problemas de desempenho devido à fragmentação de heap que notadamente têm ocorrido com o Heap do Windows.

Teste de desempenho e escalabilidade mostraram ganhos significativos na taxa de transferência de consulta durante a execução do SQL Server 2016 SP1 Analysis Services em servidores corporativos de grande porte com vários nós.


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>O que há de novo no SQL Server 2016 Analysis Services

Embora a maioria dos aprimoramentos nesta versão sejam específicos para modelos tabulares, uma série de melhorias foram desenvolvidas para modelos multidimensionais; por exemplo, a otimização da contagem distinta ROLAP para fontes de dados como DB2 e Oracle, suporte a seleção múltipla de drillthrough com Excel 2016 e otimizações em consultas do Excel.    

#### <a name="get-the-latest-tools"></a>Obtenha as ferramentas mais recentes
Para aproveitar ao máximo os aprimoramentos nesta versão, certifique-se de instalar as versões mais recentes do SSDT e SSMS.    
- [Baixar o SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)    
- [Baixar o SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)   

Se você tiver um aplicativo dependente do AMO personalizado, talvez seja necessário instalar uma versão atualizada do AMO. Para ver as instruções, consulte [Instalar provedores de dados do Analysis Services &#40;AMO, ADOMD.NET, MSOLAP&#41;](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md).    

 #### <a name="technet-virtual-labs-sql-server-2016-analysis-services"></a>Laboratórios virtuais do TechNet: SQL Server 2016 Analysis Services
Aprende melhor na prática? Acompanhe um passo a passo com as [Novidades no Laboratório Virtual do SQL Server 2016 Analysis Services](http://vlabs.holsystems.com/vlabs/technet?eng=VLabs&auth=none&src=vlabs&altadd=true&labid=23110&lod=true).
Neste laboratório, você vai criar e monitorar eventos estendidos (xEvents), atualizar um projeto tabular para o nível de compatibilidade 1200, trabalhar com as configurações do Visual Studio, implementar novos recursos de cálculo e de relação de tabela, configurar as pastas de exibição, gerenciar conversões de modelo, trabalhar com a nova TMSL (Linguagem de Script de Modelo Tabular) e com o PowerShell, além de experimentar os novos recursos do modo DirectQuery.

## <a name="modeling"></a>Modelagem    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>Desempenho de modelagem aprimorado para modelos de tabela 1200    
Para modelos de tabela 1200, as operações de metadados em SSDT são realizadas muito mais rápido do que nos modelos 1100 e 1103. Em comparação, no mesmo hardware, a criação de uma relação em um modelo definido para o nível de compatibilidade do SQL Server 2014 (1103) com 23 tabelas leva 3 segundos, enquanto a mesma relação em um modelo criado definido para o nível de compatibilidade 1200 leva pouco menos de um segundo.    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>Modelos de projeto adicionados para modelos de tabela 1200 em SSDT    
Nesta versão, você não precisa mais de duas versões do SSDT para compilar projetos do BI e relacionais. O[SQL Server Data Tools para Visual Studio 2015](http://msdn.microsoft.com/library/mt204009.aspx) adiciona modelos de projeto para soluções do Analysis Services, incluindo **Projetos de Tabela do Analysis Services** , usado para compilar modelos no nível de compatibilidade 1200. Outros modelos de projeto do Analysis Services para soluções de mineração de dados e multidimensionais também são incluídas, mas no mesmo nível funcional (1103 ou 1100) das versões anteriores.    
### <a name="display-folders"></a>Pastas de exibição
As pastas de exibição agora estão disponíveis para modelos de tabela 1200. Definidas no SQL Server Data Tools e renderizadas nos aplicativos cliente como Excel ou Power BI Desktop, as pastas de exibição ajudam a organizar grandes números de medidas em pastas individuais, adicionando uma hierarquia visual para facilitar a navegação em listas de campos.
### <a name="bi-directional-cross-filtering"></a>Filtragem cruzada bidirecional
Uma novidade nesta versão é a abordagem interna para habilitar filtros cruzados bidirecionais em modelos de tabela, o que elimina a necessidade de soluções alternativas manuais de DAX para a propagação de contextos de filtro em relações da tabela. Os filtros são gerados automaticamente apenas quando a direção pode ser estabelecida com um alto grau de certeza. Caso haja ambiguidade na forma de vários caminhos de consulta entre relações de tabela, um filtro não será criado automaticamente. Consulte [Filtros cruzados bidirecionais para modelos de tabela no SQL Server 2016 Analysis Services](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) para obter detalhes.
 ### <a name="translations"></a>Traduções    
 Agora você pode armazenar metadados traduzidos em um modelo tabular 1200. Metadados do modelo incluem campos para **Culture**, legendas traduzidas e descrições traduzidas. Para adicionar traduções, use o comando **Model** > **Translations** em [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Consulte [Traduções em modelos de tabela &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md) para ver mais detalhes.    
 ### <a name="pasted-tables"></a>Tabelas coladas    
 Agora é possível atualizar um modelo de tabela 1100 ou 1103 para 1200 quando o modelo contém tabelas coladas. É recomendável usar o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. No SSDT, defina **CompatibilityLevel** para 1200 e implante em uma instância [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter detalhes, consulte [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) .    
 ### <a name="calculated-tables-in-ssdt"></a>Tabelas calculadas no SSDT    
Uma *tabela calculada* é uma construção exclusivamente de modelos com base em uma expressão DAX ou consulta no SSDT. Quando implantada em um banco de dados, não é possível distinguir uma tabela calculada de tabelas comuns.    

 Há vários usos para tabelas calculadas, incluindo a criação de novas tabelas para expor uma tabela existente em uma função específica. O exemplo clássico é uma tabela de data que opera em vários contextos (data do pedido, data de remessa e assim por diante). Criando uma tabela calculada para uma determinada função, agora você pode ativar uma relação de tabela para facilitar consultas ou a interação de dados usando a tabela calculada. Outro uso de tabelas calculadas é combinar partes de tabelas existentes em uma tabela totalmente nova, que existe somente no modelo.  Consulte [Criar uma tabela calculada &&#40;SSAS Tabular&#41;](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md) para saber mais.    
 ### <a name="formula-fixup"></a>Correção de fórmulas    
 Com a correção de fórmulas em um modelo de tabela 1200, o SSDT atualizará automaticamente quaisquer medidas que fizerem referência a uma coluna ou tabela que tiver sido renomeada.    
 ### <a name="support-for-visual-studio-configuration-manager"></a>Suporte para o Visual Studio Configuration Manager    
 Para dar suporte a vários ambientes, como os ambientes de Teste e de Pré-produção, o Visual Studio permite aos desenvolvedores criar várias configurações de projeto usando o configuration manager. Modelos multidimensionais já tiram proveito disso, mas modelos de tabela não. Nessa versão, agora você pode usar o Configuration Manager para implantar em servidores diferentes.    

## <a name="instance-management"></a>Gerenciamento de instâncias    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>Administrar modelos tabulares 1200 no SSMS    
 Nessa versão, uma instância do Analysis Services no modo de servidor de tabela pode executar modelos de tabela em qualquer nível de compatibilidade (1100, 1103, 1200). O [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) mais recente é atualizado para exibir as propriedades e fornecer administração de modelos de banco de dados para modelos de tabela no nível de compatibilidade 1200.    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>Processamento paralelo para várias partições de tabela em modelos de tabela    
 Essa versão inclui uma nova funcionalidade de processamento paralelo para tabelas com duas ou mais partições, aumentando o desempenho de processamento. Não há nenhuma configuração para esse recurso. Para obter mais informações sobre como configurar partições e processar tabelas, consulte [Partições de modelo de tabela &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md).    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>Adicionar contas de computador como Administradores no SSMS    
 Os administradores do[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] agora podem usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para configurar contas de computador para serem membros do grupo de administradores do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Na caixa de diálogo **Selecionar Usuários ou Grupos** , defina os **Locais** para o domínio dos computadores e, em seguida, adicione o tipo de objeto **Computers** . Para obter mais informações, consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).    
 ### <a name="dbcc-for-analysis-services"></a>DBCC para Analysis Services    
 O DBCC (verificador de consistência de banco de dados) é executado internamente para detectar possíveis problemas de dados corrompidos no banco de dados de carga, mas também pode ser executado sob demanda caso você suspeite de problemas em seus dados ou modelo. O DBCC executa verificações diferentes dependendo do modelo ser tabular ou multidimensional. Veja [DBCC &#40;Verificador de Consistência de Banco de Dados&#41; para bancos de dados de tabela e multidimensionais do Analysis Services](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md) para saber mais.    
 ### <a name="extended-events-updates"></a>Atualizações de Eventos Estendidos    
 Essa versão adiciona uma interface gráfica do usuário a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para configurar e gerenciar Eventos Estendidos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Você pode configurar fluxos de dados ativos para monitorar a atividade do servidor em tempo real, manter os dados de sessão carregados na memória para análise mais rápida ou salvar fluxos de dados em um arquivo para análise offline. Para obter mais informações, consulte [Monitorar o Analysis Services com Eventos Estendidos do SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) e [Usando eventos estendidos com o Analysis Services (vídeo e postagem de blog do Guy in a Cube)](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx).    



## <a name="scripting"></a>Script
 ### <a name="powershell-for-tabular-models"></a>PowerShell para modelos de tabela    
 Esta versão inclui aprimoramentos do PowerShell para modelos de tabela no nível de compatibilidade 1200. Você pode usar todos os cmdlets aplicáveis, além de cmdlets específicos para o modo Tabular: [Invoke-ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) e [Invoke-ProcessTable](../analysis-services/powershell/invoke-processtable-cmdlet.md).    
 ### <a name="ssms-scripting-database-operations"></a>Operações de banco de dados de script de SSMS    
 No [SSMS (SQL Server Management Studio) mais recente](http://msdn.microsoft.com/library/mt238290.aspx), o script agora está habilitado para comandos de banco de dados, inclusive Create, Alter, Delete, Backup, Restore, Attach e Detach. A saída é em TMSL (linguagem de script de modelo de tabela) em JSON. Consulte [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para obter mais informações.    
 ### <a name="analysis-services-execute-ddl-task"></a>Tarefa Executar DDL do Analysis Services    
 A[Tarefa Executar DDL do Analysis Services](../integration-services/control-flow/analysis-services-execute-ddl-task.md) agora também aceita comandos de TMSL (linguagem de script de modelo de tabela).     
 ### <a name="ssas-powershell-cmdlet"></a>Cmdlet do PowerShell do SSAS    
 O cmdlet do PowerShell do SSAS **Invoke-ASCmd** agora aceita comandos de TMSL (linguagem de script de modelo de tabela). Outros cmdlets do PowerShell do SSAS serão atualizados em uma versão futura para usar os novos metadados de tabela (exceções serão indicadas nas notas de versão).    
Para obter detalhes, consulte [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) .    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>A TMSL (linguagem de script de modelo de tabela) tem suporte no SSMS    
  Usando a [versão mais recente do SSMS](http://msdn.microsoft.com/library/mt238290.aspx), agora você pode criar scripts para automatizar a maioria das tarefas administrativas para modelos de tabela 1200. Atualmente, as seguintes tarefas podem ser incluídas no script: Process em qualquer nível, além de CREATE, ALTER e DELETE no nível do banco de dados.    
    
 Funcionalmente, TMSL é equivalente à extensão de ASSL XMLA que fornece definições de objeto multidimensional, exceto pelo fato de que o TMSL usa descritores nativos como **model**, **table**e **relationship** para descrever metadados tabulares. Consulte [Referência de Linguagem de Scripts de Modelo de Tabela &#40;TMSL&#41;](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para ver mais detalhes sobre o esquema.    
    
 Um script gerado com base em JSON para um modelo de tabela pode ter a seguinte aparência:    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

A carga é um documento JSON que pode ser tão mínimo quanto o exemplo mostrado acima, ou altamente enriquecido com o conjunto completo de definições de objeto. [Referência de Linguagem de Scripts de Modelo de Tabela &#40;TMSL&#41;](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) descreve a sintaxe.

No nível do banco de dados, os comandos CREATE, ALTER e DELETE produzirão o script TMSL de saída na janela XMLA familiar.  Outros comandos, como o Process, também podem ser com script nesta versão. O suporte a scripts para muitas outras ações pode ser adicionado em uma versão futura.    

**Comandos programáveis** | **Descrição**
--------------- | ----------------
criar|Adiciona um banco de dados, conexão ou partição. O equivalente no ASSL é CREATE.
createOrReplace|Atualiza uma definição de objeto existente (banco de dados, conexão ou partição), substituindo uma versão anterior. O equivalente no ASSL é ALTER com AllowOverwrite definido para true e ObjectDefinition para ExpandFull.
excluir|Remove uma definição de objeto. O equivalente no ASSL é DELETE.
refresh|Processa o objeto. O equivalente no ASSL é PROCESS.

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>Edição de fórmula do DAX aprimorada
Atualizações para a barra de fórmulas lhe ajudarão a escrever fórmulas com mais facilidade, diferenciando funções, campos e medidas usando cores de sintaxe; ele fornece a função inteligente e sugestões de campo e informa se partes da expressão DAX estão erradas usando *rabiscos*de erro. Ele também permite que você use várias linhas (Alt + Enter) e recuo (Tab). A Barra de fórmula agora também permite que você escreva comentários como parte de suas medidas, basta digitar "//" e tudo depois desses caracteres, na mesma linha, será considerado um comentário.

### <a name="dax-variables"></a>Variáveis DAX    
Esta versão agora inclui suporte a variáveis em DAX. As variáveis agora podem armazenar o resultado de uma expressão como uma variável nomeada, que pode ser passada como um argumento para outras expressões de medida. Uma vez que os valores resultantes forem calculados para uma expressão variável, esses valores não serão alterados, mesmo se a variável for referenciada em outra expressão. Para obter mais informações, consulte [Função VAR](http://msdn.microsoft.com/library/mt243785.aspx).    
### <a name="new-dax-functions"></a>Novas funções DAX
Nessa versão, o DAX apresenta mais cinquenta novas funções para dar suporte a cálculos mais rápidos e visualizações aprimoradas no Power BI. Para saber mais, consulte [Novas funções DAX](http://msdn.microsoft.com/library/mt704075.aspx).
### <a name="save-incomplete-measures"></a>Salvar medidas incompletas
Agora você pode salvar medidas DAX incompletas diretamente em um projeto de modelo de tabela 1200 e abri-lo novamente quando você estiver pronto para continuar.
### <a name="additional-dax-enhancements"></a>Aprimoramentos DAX adicionais
- Cálculo de não vazio: reduz o número de verificações necessárias para não vazio.
- Fusão de medida: várias medidas da mesma tabela são combinados em um único mecanismo de armazenamento (consulta).
- Agrupar conjuntos: quando uma consulta pede medidas em diversas granularidades (Total/Ano/Mês), uma única consulta é enviada no nível mais baixo e o restante das granularidades são derivadas do nível mais baixo.     
- Eliminação de junção redundante: uma consulta única para o mecanismo de armazenamento retorna as colunas de dimensão e os valores de medida.
- Avaliação estrita de IF/SWITCH: uma ramificação cuja condição é falsa não resultará em consultas do mecanismo de armazenamento. Anteriormente, as ramificações foram avaliadas adiantadamente, mas os resultados eram descartados posteriormente.     
    
## <a name="developer"></a>Desenvolvedor    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>Namespace Microsoft.AnalysisServices.Tabular para programação de 1200 tabular no AMO
 O AMO (Analysis Services Management Objects) é atualizado para incluir um novo namespace tabular para gerenciar uma instância do Modo Tabular do SQL Server 2016 Analysis Services, bem como fornecer a linguagem de definição de dados para a criação ou modificação de modelos de tabela 1200 programaticamente. Visite [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) para ler sobre a API.    
 ### <a name="analysis-services-management-objects-amo-updates"></a>Atualizações do AMO (Objetos de Gerenciamento do Analysis Services)
 Os [Objetos de Gerenciamento do Analysis Services &#40;AMO&#41;](http://msdn.microsoft.com/library/mt436122.aspx) foram refatorados para incluir um segundo assembly, Microsoft.AnalysisServices.Core.dll. O novo assembly separa as classes comuns como Server, Database e Roles que têm ampla aplicação no Analysis Services, independentemente do modo de servidor.    
    
 Anteriormente, essas classes eram parte do assembly Microsoft.AnalysisServices original. Movê-las para um novo assembly abre caminho para extensões futuras para o AMO, com divisão clara entre as APIs genéricas e as de contexto específico.    
    
 Os aplicativos existentes não são afetados pelos novos assemblies. No entanto, se você optar por recompilar os aplicativos que usam o novo assembly do AMO por qualquer motivo, certifique-se de adicionar uma referência ao Microsoft.AnalysisServices.Core.    
    
 De modo similar, os scripts do PowerShell que carregam e chamam o AMO agora devem carregar o Microsoft.AnalysisServices.Core.dll. Certifique-se de atualizar todos os scripts.  

### <a name="json-editor-for-bim-files"></a>Editor de JSON para arquivos BIM
A Exibição de Código no Visual Studio 2015 agora renderiza o arquivo BIM no formato JSON para modelos de tabela 1200. A versão do Visual Studio determina se o arquivo BIM é renderizado em JSON por meio do Editor de JSON interno ou como texto simples.

Para usar o editor de JSON, com a capacidade de expandir e recolher seções do modelo, será necessária a versão mais recente do SQL Server Data Tools e o Visual Studio 2015 (qualquer edição, incluindo a Community edition gratuita). Para todas as outras versões do SSDT ou Visual Studio, o arquivo BIM é renderizado em JSON como texto simples.
Um modelo vazio conterá, no mínimo, o JSON a seguir:

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]    
> Evite editar o JSON diretamente. Fazer isso pode corromper o modelo.    
 ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>Novos elementos no esquema MS-CSDLBI 2.0    
 Os elementos a seguir foram adicionados ao tipo complexo **TProperty** definido no esquema [MS-CSDLBI] 2.0:    
    
|Elemento|Definição|    
|-------------|----------------|    
|DefaultValue|Uma propriedade que especifica o valor usado ao avaliar a consulta. A propriedade DefaultValue é opcional, mas ela será selecionada automaticamente se os valores do membro não puderem ser agregados.|    
|Estatísticas|Um conjunto de estatísticas dos dados subjacentes que está associado à coluna. Essas estatísticas são definidas pelo tipo complexo TPropertyStatistics e serão fornecidas apenas se elas não forem computacionalmente caras para gerar, conforme descrito na seção 2.1.13.5 do documento Formato de Arquivo de Definição de Esquema Conceitual com Anotações de Business Intelligence.|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>Nova implementação do DirectQuery    
Esta versão traz melhorias significativas no DirectQuery para modelos de tabela 1200. Aqui está um resumo:    
-   O DirectQuery agora gera consultas mais simples, que fornecem um melhor desempenho.    
-   Controle adicional sobre a definição de conjuntos de dados de exemplo usado para teste e design de modelos.    
-   A RLS (segurança em nível de linha) agora tem suporte em modelos 1200 no modo DirectQuery. Anteriormente, a presença da RLS evitava a implantação de um modelo de tabela no modo DirectQuery.    
-   As colunas calculadas agora têm suporte em modelos tabulares 1200 no modo DirectQuery. Anteriormente, a presença de colunas calculadas evitava a implantação de um modelo de tabela no modo DirectQuery.    
-   Otimizações de desempenho incluem a eliminação de junções redundantes para VertiPaq e DirectQuery. 

### <a name="new-data-sources-for-directquery-mode"></a>Novas fontes de dados para o modo DirectQuery    
 Fontes de dados com suporte para modelos de tabela 1200 no modo DirectQuery agora incluem o Oracle, Teradata e plataforma de análise do Microsoft (anteriormente conhecido como Parallel Data Warehouse).    
    
Para saber mais, consulte [Modo DirectQuery &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).    

## <a name="see-also"></a>Consulte também
[Blog da equipe do Analysis Services](http://blogs.msdn.microsoft.com/analysisservices/)    
[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)    
     


