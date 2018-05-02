---
title: Caixas de diálogo do SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 07/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.pro.traceproperties.general.f1;
- sql13.pro.traceproperties.eventsselection.f1;
- sql13.pro.traceproperties.eventsselection.f1
- sql13.pro.traceproperties.general.f1
- sql13.pro.tracetemplateproperties
- sql13.pro.edittracetemplateproperties.general.f1
- sql13.pro.edittracetemplateproperties.eventsselection.f1
- sql13.pro.tracefileproperties.general.f1
- sql13.pro.tracefileproperties.eventsselection.f1
- sql13.pro.performancecounterlimit.f1
- sql13.pro.replay.tools.generaloptions.f1
- sql13.pro.replay.tools.sourcetable.f1
- sql13.pro.replay.tools.destinationtable.f1
- sql13.pro.replay.generaloptions.f1
- sql13.pro.replay.generaloptions.advanced.f1
- sql13.pro.find.f1
- sql13.pro.organize.columns.f1
- sql13.pro.editfilter.f1
helpviewer_keywords:
- Profiler [SQL Server Profiler], help
- SQL Server Profiler, help
- Trace Properties dialog box
- Trace Template Properties dialog box
- Trace Files Properties dialog box
- Performance Counters List dialog box
- General Options dialog box
- Select Workload Table dialog box
- Destination Table dialog box
- Replay Configuration dialog box
- Find dialog box
ms.assetid: e57b9160-4b78-4353-abb2-bfdbdf523d7a
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 284333202ee48153b0de4d513502e35edc73acaf
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="sql-server-profiler-dialog-boxes"></a>Caixas de diálogo do SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] O Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é uma ferramenta que captura eventos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um servidor. Os eventos são salvos em um arquivo de rastreamento que posteriormente pode ser analisado ou utilizado para reproduzir uma série específica de etapas na tentativa de diagnosticar um problema. Estes são os comandos e configurações disponíveis nas caixas de diálogo de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
## <a name="trace-properties"></a>Propriedades do rastreamento
### <a name="general-tab"></a>Guia Geral
Use a guia **Geral** da caixa de diálogo **Propriedades do Rastreamento** para exibir ou especificar propriedades de um rastreamento.  
|Item|Description
|---|---
|**Nome do rastreamento** |Especifique o nome do rastreamento.  
|**Nome do provedor de rastreamento**|Exibe o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que será rastreada. Esse campo é populado automaticamente com o nome do servidor que você especificou ao se conectar. Para alterar o nome do provedor de rastreamento, clique em **Cancelar** para fechar a caixa de diálogo e iniciar um novo rastreamento.  
|**Tipo de provedor de rastreamento**|Exibe o tipo de servidor que está fornecendo o rastreamento. O arquivo de definição de rastreamento popula o campo **Tipo de provedor de rastreamento** automaticamente. Não é possível modificar esse campo.  
|**version**|Exibe a versão do servidor que está fornecendo o rastreamento. O arquivo de definição de rastreamento popula o campo **Versão** automaticamente. Não é possível modificar esse campo.  
|**Usar o modelo**|Selecione um modelo do diretório modelo. O diretório é populado com os modelos padrões e qualquer modelo definido pelo usuário, criados para o tipo de provedor de rastreamento atual.  
|**Salvar no arquivo**|Capture os dados de rastreamento para um arquivo .trc. Salvar dados de rastreamento é útil para revisão e análise posteriores.  
|**Definir tamanho máximo do arquivo (MB)**|Se você optar por salvar os dados de rastreamento em um arquivo, especifique o tamanho máximo do arquivo de rastreamento. O padrão é 5 MB (megabytes). O tamanho máximo é limitado somente pelo sistema de arquivos (NTFS, FAT) onde o arquivo é salvo.  
|**Salvar como**|Depois de selecionar para salvar, é possível selecionar esse ícone para alterar o nome de arquivo.  
|**Habilitar substituição de arquivo**|Selecione para habilitar a criação de arquivos adicionais para aceitar os dados de rastreamento, quando o tamanho máximo de arquivo for atingido. Cada nome de arquivo novo consiste do nome de arquivo .trc original, numerado em sequência. Por exemplo, ao alcançar o tamanho máximo do arquivo, **NewTrace.trc** é fechado e um novo arquivo **NewTrace_1.trc**é aberto, seguido de **NewTrace_2.trc**e assim por diante. A substituição de arquivos é habilitada por padrão quando você salvar um rastreamento em um arquivo.  
|**Dados de rastreamento de processos do servidor**|Especifique que o servidor que executa o rastreamento deve processar os dados de rastreamento. Usando essa opção a sobrecarga de desempenho devido ao rastreamento é reduzida. Se selecionada, nenhum evento é ignorado mesmo sob condições de tensão. Se essa caixa de seleção for desmarcada, o processamento será executado pelo SQL Server Profiler, e há uma possibilidade de que alguns eventos não sejam rastreados sob condições de tensão.  
|**Salvar na tabela**|Capture os dados de rastreamento para uma tabela de banco de dados. Salvar dados de rastreamento é útil para revisão e análise posteriores. Entretanto, ao salvar dados de rastreamento para uma tabela isso pode levar a uma sobrecarga significativa no servidor no qual o rastreamento está sendo salvo. Se possível, não salve a tabela de rastreamento no mesmo servidor que está sendo rastreado.  
|**Tabela de destino**|Depois de selecionar para salvar os dados de rastreamento para uma tabela de banco de dados, é possível selecionar esse ícone para alterar o nome da tabela.  
| **Definir máximo de linhas (em milhares)**|Especifique o número maior de linhas nas quais salvar dados. O padrão é 1000 linhas. 
|**Habilitar horário de parada do rastreamento**|Defina a data e hora para o rastreamento ser concluído e se fechar. 

### <a name="events-selection-tab"></a>Guia seleção de eventos
Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** para exibir ou especificar eventos do rastreamento e colunas de dados.  
|Item|Description
|---|---
|Coluna**Eventos** |Especifique os eventos do rastreamento marcando ou desmarcando a caixa de seleção na coluna de eventos. Os**Eventos** são organizados por categoria de evento. As classes de evento especificadas no modelo são selecionadas automaticamente. Para obter mais informações, confira [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
|Colunas de dados|Especifique as colunas de dados do rastreamento marcando a caixa correspondente ao evento e a coluna de dados necessária. Por padrão, todas as colunas de dados pertinentes são marcadas para cada evento incluído no rastreamento.  
|Filtros|Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** . Para obter mais informações, consulte [SQL Server Profiler - Editar Filtro](http://msdn.microsoft.com/library/a589eff5-6ec6-4f6e-94b8-831658257f14).  
|**Mostrar todos os eventos**|Mostra todos os eventos disponíveis. Por padrão, somente as linhas selecionadas na grade **Seleção de Eventos** são exibidas. Desmarque essa caixa para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** .  
|**Mostrar todas as colunas**|Mostra todas as colunas de dados disponíveis. Por padrão, somente colunas de dados selecionadas são exibidas. Desmarque essa caixa para ocultar todas as colunas de dados não selecionadas na grade **Seleção de Eventos** .  
|**Filtros de coluna**|Abre a caixa de diálogo **Editar Filtro** . Você pode usar essa caixa de diálogo para editar filtros de coluna de dados.  
|**Organizar Colunas**|Altera a ordem das colunas no rastreamento e agrupa os resultados em uma ou mais colunas.  

## <a name="trace-template-properties"></a>Propriedades do modelo de rastreamento 
### <a name="new-general-tab"></a>Novo (guia Geral)
Use a guia **Geral** da caixa de diálogo **Propriedades do Modelo de Rastreamento** para criar novos modelos de rastreamento usando as opções a seguir. Para acessar essa caixa de diálogo, no menu **Arquivo** do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] aponte para **Modelos** e clique em **Novo**.
|Item|Description
|---|---
|**Selecionar tipo de servidor**|Especifique o tipo de servidor em relação ao qual esse modelo será usado.  
|**Novo nome do modelo**|Forneça um nome descritivo para o modelo.  
|**Basear novo modelo no existente**|Use um modelo da lista como base para esse modelo. Todos os eventos selecionados, colunas de dados e filtros inicialmente correspondem aos do modelo existente e podem, depois, ser modificados conforme necessário.  
|**Usar como modelo padrão para o tipo de servidor selecionado**|Use esse modelo por padrão para rastreamentos criados para esse tipo de servidor.  

### <a name="edit-general-tab"></a>Editar (guia Geral)
 Use a guia **Geral** da caixa de diálogo **Propriedades do Modelo de Rastreamento** para visualizar ou editar modelos de rastreamento existentes usando as seguintes opções. Para acessar essa caixa de diálogo, no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **do** , aponte para **Modelos**e clique em **Editar Modelo**.  
|Item|Description
|---|---
|**Selecionar tipo de servidor**|Especifique o tipo de servidor em relação ao qual esse modelo será usado.  
|**Selecionar Nome do Modelo**|Selecione o modelo que você deseja editar.  
|**Usar como modelo padrão para o tipo de servidor selecionado**|Use esse modelo por padrão para rastreamentos criados para esse tipo de servidor.  

### <a name="events-selection-tab"></a>Guia seleção de eventos
Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Modelo de Rastreamento** para exibir, editar ou especificar classes de evento e colunas de dados para incluir um modelo de rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
|Item|Description
|---|---
|Coluna**Eventos** |Especifique os eventos que devem ser rastreados selecionando ou desmarcando a caixa de seleção na coluna Eventos. Os eventos são organizados por categoria de evento. Se você selecionou **Basear novo modelo no existente** na guia **Geral** , os eventos serão selecionados automaticamente de acordo com o modelo especificado. Para obter mais informações sobre classes de evento, consulte [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
|Colunas de dados|Especifique as colunas de dados que devem ser rastreadas marcando a caixa que corresponde ao evento e a coluna de dados que você precisa. Todas as colunas de evento pertinentes serão selecionadas por padrão para cada evento incluído no rastreamento, se a caixa de seleção correspondente ao evento estiver marcada. Se você selecionou **Basear novo modelo no existente** na guia **Geral** , as colunas de dados e os filtros serão selecionados automaticamente de acordo com o modelo especificado.  
|Filtros|Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** .  
|**Mostrar todos os eventos**|Mostra todos os eventos disponíveis. Essa opção será selecionada por padrão se você estiver criando um novo modelo que não seja baseado em um modelo existente. Desmarque para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** .  
|**Mostrar todas as colunas**|Mostra todas as colunas de dados disponíveis. Essa opção será selecionada por padrão se você estiver criando um novo modelo que não seja baseado em um modelo existente. Desmarque para ocultar todas as colunas de dados não selecionadas na guia **Seleção de Eventos** .  
|**Filtros de coluna**|Inicia a caixa de diálogo **Editar Filtro**, que exibe um ícone de filtro à esquerda do rótulo da coluna de dados. Use a caixa de diálogo **Editar Filtro** para editar filtros de coluna de dados.  
|**Organizar Colunas**|Altera a ordem das colunas no rastreamento e agrupa os resultados em uma ou mais colunas. 
## <a name="trace-file-properties"></a>Propriedades do arquivo de rastreamento 
### <a name="general-tab"></a>Guia Geral
Use a guia **Geral** da caixa de diálogo **Propriedades do Arquivo de Rastreamento** para exibir as propriedades de um arquivo de rastreamento.  
Para exibir essa janela, abra um arquivo de rastreamento. Em seguida, no menu **Arquivo** , clique em **Propriedades**.  
|Item|Description
|---|---
|**Nome do arquivo**|O caminho e o nome do arquivo de rastreamento exibido.  
|**Nome do provedor de rastreamento**|Exibe o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foi rastreada.  
|**Tipo de provedor de rastreamento**|Mostra o tipo de servidor que forneceu o rastreamento.  
|**version**|Exibe a versão do servidor que forneceu o rastreamento.  
|**Tamanho do arquivo (KB)**|O tamanho do arquivo de rastreamento em kilobyte (KB).  
|**Criado**|A data e hora em que o arquivo de rastreamento foi criado.  
|**Modificado** |A data e hora em que o arquivo de rastreamento foi modificado.  
### <a name="events-selection-tab"></a>Guia seleção de eventos
Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Arquivo de Rastreamento** para exibir as propriedades da coluna do rastreamento ou remover colunas de dados do rastreamento.  
Para exibir essa janela, abra um arquivo de rastreamento. Em seguida, no menu **Arquivo** , clique em **Propriedades**e, então, clique na guia **Seleção de Eventos** .  
|Item|Description
|---|---
|Coluna**Eventos** |Exiba eventos rastreados organizados por categoria de evento. Inicialmente, todos os eventos no rastreamento são selecionados. Eventos podem ser selecionados marcando a caixa ou uma coluna de dados referente a um evento. Se a caixa do evento estiver marcada, todas as colunas de dados disponíveis desse evento serão selecionadas. Se a coluna de dados de um evento estiver marcada, o evento será marcado e qualquer outra coluna necessária também será automaticamente marcada. Se você estiver exibindo uma tabela ou arquivo de rastreamento, desmarcar as caixas de seleção de eventos ou colunas de dados reduzirá o total de dados visíveis na janela de rastreamento para uma análise mais fácil. Você também pode alterar os filtros de coluna para reduzir o total de dados visíveis na janela de rastreamento. Para obter mais informações sobre classes de evento, consulte [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
|Colunas de dados|Exiba colunas de dados rastreadas. Todas as colunas de dados pertinentes no rastreamento são selecionadas por padrão para cada evento incluído no rastreamento.  
|Filtros|Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** .  
|**Mostrar todos os eventos**|Mostra todos os eventos disponíveis. Por padrão, somente as linhas selecionadas na grade **Seleção de Eventos** são exibidas. Desmarque essa caixa para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** . Se a opção **Mostrar todos os eventos** estiver marcada e você estiver visualizando uma tabela ou arquivo de rastreamento, todos os eventos que foram gravados no rastreamento serão exibidos na janela de rastreamento.  
|**Mostrar todas as colunas**|Mostra todas as colunas de dados disponíveis. Por padrão, somente colunas de dados selecionadas são exibidas. Desmarque essa caixa para ocultar todas as colunas de dados não selecionadas na grade **Seleção de Eventos** .  
|**Filtros de coluna**|Inicia a caixa de diálogo **Editar Filtro** , que exibe um ícone de filtro à esquerda do rótulo da coluna para colunas de dados filtrados. Use a caixa de diálogo **Editar Filtro** para editar filtros de coluna de dados.  
|**Organizar Colunas**|Depois de selecionar **Eventos** e colunas de dados a serem rastreados, clique em **Organizar Colunas** para forçar a grade a reclassificar a coluna na janela de resultados do rastreamento.  
## <a name="trace-table-properties"></a>Propriedades da tabela de rastreamento
### <a name="events-selection-tab"></a>Guia seleção de eventos
Use a guia **Seleção de Eventos** da caixa de diálogo **Propriedades da Tabela de Rastreamento** para exibir eventos e propriedades da coluna de dados do rastreamento ou para remover eventos ou colunas do rastreamento.  
Para visualizar esta janela, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para abrir uma tabela de rastreamento. Em seguida, no menu **Arquivo** , clique em **Propriedades**e na guia **Seleção de Eventos** .  
|Item|Description
|---|---
|Coluna**Eventos** |Exiba eventos rastreados organizados por categoria de evento. Eventos podem ser selecionados marcando a caixa ou uma coluna de dados referente a um evento. Se a caixa do evento estiver marcada, todas as colunas de dados disponíveis desse evento serão selecionadas. Se a coluna de dados de um evento estiver marcada, o evento será marcado e qualquer outra coluna necessária também será automaticamente marcada. Se você estiver exibindo uma tabela ou arquivo de rastreamento, desmarcar as caixas de seleção de eventos ou colunas de dados reduzirá o total de dados visíveis na janela de rastreamento para uma análise mais fácil. Você também pode alterar os filtros de coluna para reduzir o total de dados visíveis na janela de rastreamento. Para obter mais informações sobre classes de evento, consulte [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
|Outras colunas de dados|Exiba colunas de dados rastreadas. Todas as colunas de dados pertinentes no rastreamento são selecionadas por padrão para cada evento incluído no rastreamento.  
|Filtros|Especifique os filtros clicando no cabeçalho da coluna de dados e digitando os critérios de filtro. As colunas de dados filtrados são indicadas por um ícone de filtro à esquerda do rótulo da coluna na caixa de diálogo **Editar Filtro** .  
|**Mostrar todos os eventos**|Mostra todos os eventos disponíveis. Por padrão, somente as linhas selecionadas na grade **Seleção de Eventos** são exibidas. Desmarque essa caixa para ocultar todos os eventos não selecionados na grade **Seleção de Eventos** . Se a opção **Mostrar todos os eventos** estiver marcada e você estiver visualizando uma tabela ou arquivo de rastreamento, todos os eventos que foram gravados no rastreamento serão exibidos na janela de rastreamento.  
|**Mostrar todas as colunas**|Mostra todas as colunas de dados disponíveis. Por padrão, somente colunas de dados selecionadas são exibidas. Desmarque essa caixa para ocultar todas as colunas de dados não selecionadas na grade **Seleção de Eventos** .  
|**Filtros de coluna**|Inicia a caixa de diálogo **Editar Filtro**, que exibe um ícone de filtro à esquerda do rótulo da coluna. Você pode usar essa caixa de diálogo para editar filtros de coluna de dados.  
|**Organizar Colunas** |Depois de selecionar **Eventos** e colunas de dados a serem rastreados, clique em **Organizar Colunas** para forçar a grade a reclassificar a coluna na janela de resultados do rastreamento.  
## <a name="performance-counters-limit"></a>Limite de contadores de desempenho
Use a caixa de diálogo Limite de Contadores de Desempenho para limitar as informações de um arquivo de log de desempenho do Monitor do Sistema ao correlacioná-lo com um rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Você pode usar essa caixa de diálogo para selecionar os contadores que devem ser exibidos e usados para a correlação.  
A caixa de diálogo **Limite de Contadores de Desempenho** é populada com objetos e contadores de desempenho contidos no arquivo de log de desempenho.  
### <a name="to-select-performance-objects-and-counters-to-correlate-with-a-trace"></a>Para selecionar objetos e contadores de desempenho a correlacionar com um rastreamento  
1.  Expanda um objeto de desempenho para verificar quais contadores estão incluídos no arquivo de log de desempenho.  
2.  Verifique os contadores que você deseja correlacionar com o arquivo de rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  

Para selecionar todos os contadores de um objeto de desempenho, marque a caixa adjacente ao objeto. Marcando o nó mais alto, que indica o computador, você seleciona todos os objetos e contadores de desempenho contidos no arquivo de log de desempenho. 
## <a name="toolsoptions-general-options-page"></a>Ferramentas/Opções (página Opções gerais)
Use a caixa de diálogo **Opções Gerais** para exibir ou especificar as opções a seguir.  
### <a name="display-options"></a>Opções de exibição  
|Item|Description
|---|---
|**Nome da fonte**|Exibe o nome da fonte usada na grade de resultados de rastreamento durante rastreamentos.  
|**Tamanho da fonte**|Exibe o tamanho da fonte usada na grade de resultados de rastreamento durante rastreamentos.  
|**Escolher Fonte**|Abre uma caixa de diálogo para alterar as configurações de fonte.  
|**Usar configurações regionais para exibir valores de data e hora**|Exibe os valores de data e hora com os parâmetros regionais configurados para seu computador. Se você não selecionar essa opção, os valores de data e hora serão exibidos no formato fixo usado pelo Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]que inclui milissegundos. Observe que a ativação/desativação desta caixa de seleção altera o formato de exibição das colunas de hora como **StartTime** e **EndTime**. Porém, não altera os parâmetros de valores **DateTime** dentro dos eventos de idioma ou RPCs (chamadas de procedimento remoto).  
|**Mostrar valores na coluna Duration em microssegundos**|Exibe os valores em microssegundos na coluna de dados **Duration** de rastreamentos. Por padrão, a coluna **Duration** exibe valores em milissegundos.  
### <a name="tracing-options"></a>Opções de rastreamento  
|Item|Description
|---|---
|**Iniciar rastreamento imediatamente após estabelecer a conexão.**|Começa a rastrear usando o modelo padrão assim que uma conexão é estabelecida.  
|**Atualizar a definição de rastreamento quando a versão do provedor for alterada**|Aplica a definição de rastreamento mais recente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o provedor for atualizado. Este item não é verificado por padrão. Isso força o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] a consultar o servidor quanto à definição de rastreamento e a recriar o arquivo em disco, se houver um.  
### <a name="file-rollover-options"></a>Opções de sobreposição de arquivo  
|Item|Description
|---|---
|**Carregar todos os arquivos de substituição em sequência, sem avisar**|Carrega automaticamente os arquivos de substituição quando um arquivo de rastreamento é aberto. Se mais de um arquivo foi criado durante o rastreamento, selecionar esta opção carregará automaticamente todos os arquivos de substituição.  
|**Perguntar antes de carregar arquivos de substituição**|O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pergunta antes de adicionar um arquivo de substituição quando um arquivo de rastreamento é aberto.  
|**Nunca carregar arquivos de substituição subsequentes**|O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] nunca carrega arquivos de substituição subsequentes quando um arquivo de rastreamento é aberto.  
### <a name="replay-options"></a>Opções de reprodução  
|Item|Description
|---|---
|**Número padrão de threads de repetição**|Especifica o número de threads de repetição a usar simultaneamente. Um número mais alto consome mais recursos durante a repetição, porém aumenta a simultaneidade da repetição.  
|**Intervalo de espera padrão do monitor de integridade (s)**|Especifica o intervalo de espera de repetição, em segundos. O padrão é 3600 segundos (1 hora). Esta configuração afeta o tempo durante o qual um thread pode ser executado antes de ser concluído pelo monitor de integridade.  
|**Intervalo de sondagem padrão do monitor de integridade (s)**|Especifica o intervalo de sondagem do monitor de integridade durante a repetição, em segundos. O padrão é 60 segundos. Este valor permite que o usuário configure com que frequência o monitor de integridade sonda candidatos a conclusão.
## <a name="source-table-database-engine-tuning-advisor-select-workload-table"></a>Tabela de origem (tabela de carga de trabalho selecionada do Orientador de Otimização do Mecanismo de Banco de Dados)
O Microsoft SQL Server Profiler e o Orientador de Otimização usam essa caixa de diálogo para selecionar tabelas.  
- No Profiler, use a caixa de diálogo **Tabela de Origem** para especificar uma tabela de origem para uma tabela de rastreamento. Essa é uma tabela a partir da qual é carregado um rastreamento e cujo conteúdo é exibido ou usado para repetir o rastreamento.  
- No Orientador de Otimização, use a caixa de diálogo **Selecionar Tabela de Carga de Trabalho** para selecionar uma tabela de banco de dados que contém informações de rastreamento do criador de perfil para usar como uma carga de trabalho de otimização ou para visualizar o conteúdo da tabela antes de iniciar a análise de otimização.  

|Item|Description
|---|---
|**SQL Server**|Especifica a instância do SQL Server conectada atualmente. Esse campo é populado automaticamente e não pode ser atualizado.  
|**Backup de banco de dados**|Especifique o banco de dados onde está localizada a tabela de rastreamento.  
|**Proprietário**|Specifies the owner of the trace table. Este campo é populado automaticamente como **dbo**.  
|**Table**|Especifique o nome da tabela de rastreamento a partir da qual deve ser lido o rastreamento.  
## <a name="destination-table"></a>Tabela de destino
Use a caixa de diálogo **Tabela de Destino** para especificar uma tabela em que você deseja armazenar o rastreamento.  
|Item|Description
|---|---
|**SQL Server**|Especifica a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectada atualmente. Esse campo é populado automaticamente e não pode ser atualizado. Para alterar o servidor, clique em **Cancelar** e se conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você deseja armazenar a tabela de rastreamento.  
|**Backup de banco de dados**|Especifica o banco de dados em que você quer armazenar a tabela de rastreamento.  
|**Proprietário**|Specifies the owner of the trace table. Este campo é populado automaticamente como **dbo**.  
|**Table**|Especifica o nome da tabela em que você quer armazenar o rastreamento.  
## <a name="replay-configuration"></a>Configuração de reprodução
### <a name="basic-replay-options"></a>Opções de reprodução básicas
Na caixa de diálogo **Configuração de Repetição** , use a página **Opções de Repetição Básicas** para especificar como repetir um arquivo ou tabela de rastreamento.  
Para exibir essa janela, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para abrir um arquivo ou tabela de rastreamento que contenha os eventos adequados para repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md). Enquanto o arquivo ou tabela de rastreamento está aberto, no menu **Repetição** , clique em **Iniciar**e, então, conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde deseja repetir o rastreamento.  
|Item|Description
|---|---
|**Servidor de repetição**|Exibe a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar para a repetição.  
|**Alterar...**|Inicia a caixa de diálogo **Conectar ao Servidor** para conectar a outro servidor.  
|**Salvar no arquivo** |Salva os resultados da repetição para um arquivo. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibe o diálogo de arquivo padrão, permitindo que se especifique o local para salvar o arquivo.  
|**Salvar na tabela**|Salva os resultados da repetição em uma tabela. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibe a caixa de diálogo de seleção da tabela, permitindo que se especifique o local para salvar a tabela.  
|**Número de threads de repetição**|Especifica o número de threads de repetição a usar simultaneamente. Um número maior consome mais recursos durante a repetição, porém esta será mais rápida e simultânea.  
|**Repetir eventos na ordem em que foram rastreados**|Repete os eventos sequencialmente. Use esta opção se você estiver repetindo um rastreamento para depuração.  
|**Reproduzir eventos usando vários threads** |Repete os eventos simultaneamente. Essa opção é mais rápida que repetir eventos sequencialmente, mas desabilita a depuração. Os eventos são ordenados dentro de seus identificadores de processo de sistema (SPID).  
|**Exibir resultados da repetição**|Exibe os resultados da repetição no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. 
### <a name="advanced-replay-options"></a>Opções de reprodução avançadas
Na caixa de diálogo **Configuração de Reprodução** , use a guia **Opções de Reprodução Avançadas** para especificar como reproduzir um arquivo de rastreamento.  
Para exibir essa janela, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para abrir um arquivo ou tabela de rastreamento que contenha os eventos adequados para repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md). Enquanto o arquivo ou tabela de rastreamento está aberto, no menu **Reprodução** , clique em **Iniciar**, conecte-se à instância do SQL Server em que você deseja reproduzir o rastreamento e clique na guia **Opções de Reprodução Avançadas** .  
|Item|Description
|---|---
|**Repetir SPIDs do sistema**|Especifica se o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] repete os identificadores de processos do sistema (SPIDs).  
|**Repetir somente um SPID**|Repete apenas a atividade no arquivo de rastreamento de origem que está relacionado ao SPID selecionado.  
|**SPID para repetir**|Especifica o SPID para repetir.  
|**Limitar repetição por data e hora**|Verifica para repetir apenas uma parte do arquivo de rastreamento de origem.  
|**Hora de início**|Data e hora no arquivo de rastreamento de origem em que a repetição deve iniciar.  
|**Hora de término**|Data e hora no arquivo de rastreamento de origem em que a repetição deve ser interrompida.  
|**Intervalo de espera do monitor de integridade (s)**|Especifica o intervalo de espera de repetição, em segundos. O padrão é 3600 segundos (1 hora). Essa configuração afeta o tempo durante o qual um processo pode ser executado antes de ser concluído pelo monitor de integridade.  
|**Intervalo de sondagem do monitor de integridade (s)**|Especifica o intervalo de sondagem do monitor de integridade durante a repetição, em segundos. O padrão é 60 segundos. Este valor permite que o usuário configure com que frequência o monitor de integridade sonda candidatos a conclusão.  
|**Habilitar monitor de processos bloqueados do SQL Server**|Habilita um processo que procura processos bloqueados ou em bloqueio.  
|**Intervalo de espera do monitor de processos bloqueados (s)**|Configura a frequência com que o monitor de processos bloqueados procura processos bloqueados ou em bloqueio.  
## <a name="find-dialog-box"></a>Caixa de diálogo Localizar
Use a caixa de diálogo **Localizar** para pesquisar um rastreamento para caracteres ou palavras específicos. Para cancelar uma pesquisa em andamento, pressione ESC.  
 Para abrir essa caixa de diálogo no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], no menu **Editar** , clique em **Localizar**.  
|Item|Description
|---|---
|**Localizar**|Insira o texto que deseja pesquisar. A pesquisa corresponde a qualquer cadeia de caracteres que contenha a cadeia especificada. Por exemplo, a pesquisa por "Concluído" corresponde a "SQL:LoteConcluído". Caracteres curinga (*, ?, etc.) não têm suporte.  
|**Pesquisar na coluna**|Clique em uma coluna de dados para pesquisar ou em **\<Todas as colunas>** para pesquisar todas as colunas de dados no rastreamento.  
|**Diferenciar maiúsculas de minúsculas**|Localiza texto que tem maiúsculas e minúsculas iguais às da caixa **Localizar** . Desmarque essa caixa de seleção para localizar exemplos no rastreamento que tenham caracteres de texto tanto com letras maiúsculas como com minúsculas.  
|**Coincidir palavra inteira**|Restringe a pesquisa a palavras inteiras. Desmarque a caixa de seleção **Coincidir palavra inteira** para pesquisar caracteres em uma palavra.  
|**Localizar Próximo**|Localiza o próximo exemplo dos caracteres na caixa **Localizar** .  
|**Localizar Anterior**|Pesquisa para trás no rastreamento, para localizar o exemplo anterior dos caracteres na caixa **Localizar** .  
 ## <a name="organize-columns"></a>Organizar colunas
Use a caixa de diálogo **Organizar Colunas** para selecionar colunas de dados para agrupar ou agregar eventos exibidos em um rastreamento, o que torna os arquivos ou tabelas de rastreamento grandes mais fáceis de exibir e analisar.  
- A agregação movimenta e recolhe todos os eventos no rastreamento em seu respectivo tipo de classe de evento. Um sinal de adição (**+**) é exibido à esquerda do nome de classe de evento. Clicando no sinal de mais, você expande a classe de evento para exibir todos os eventos desse tipo.  
- O agrupamento organiza todas as classes de evento de um tipo específico juntando-as na janela de rastreamento. Porém, os eventos não são recolhidos sob o tipo de classe de evento.  

Quando você agrupa ou agrega eventos em uma janela de rastreamento, as colunas selecionadas para agrupamento ou agregação permanecem fixas na janela de exibição, mas é possível rolar para a direita ou esquerda a fim de exibir todas as outras colunas de dados.  
Para acessar essa caixa de diálogo, abra um arquivo ou tabela de rastreamento existente e clique em **Propriedades** no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **do** . Na caixa de diálogo **Propriedades do Rastreamento** , clique na guia **Seleção de Eventos** e em **Organizar Colunas**. Você também pode clicar em **Organizar Colunas** na guia **Seleção de Eventos** ao criar um rastreamento novo.  
Mova os nomes da coluna de dados sob **Grupos** para agrupar ou agregar classes de evento na janela de rastreamento.
- Para agregar eventos, mova uma coluna de dados para **Grupos**. Com isso, todos os eventos de um tipo específico são recolhidos abaixo do nome do tipo de classe de evento na janela de rastreamento. Um sinal de adição (**+**) é exibido à esquerda do nome de classe de evento. Clique no sinal de mais para expandir o tipo de classe de evento e exibir todos os eventos. Você pode ativar e desativar a agregação e o agrupamento clicando em **Exibição Agregada** ou **Exibição Agrupada** no menu **Exibição** .
- Para agrupar eventos, mova mais de uma coluna de dados para **Grupos**. Com isso, todos os eventos de um tipo específico são agrupados na janela de rastreamento, mas os eventos não são recolhidos abaixo do nome de cada tipo de classe de evento. Você pode alternar entre exibições agrupadas e não agrupadas clicando em **Exibição Agrupada** no menu Exibição. Quando mais de uma coluna de dados é movida para **Grupos**, a opção de alternar para a **Exibição Agregada** fica indisponível.

|Item|Description
|---|---
|**Colunas**|Lista de colunas de dados disponíveis para serem movidas para **Grupos**. Clique no sinal de adição (**+**) à esquerda de **Colunas** para expandir a lista.  
|**Para cima**|Depois de selecionar uma coluna de dados, clique em **Para Cima** para mover colunas de dados para **Grupos**. Você também pode clicar em **Acima** para reorganizar a exibição de colunas na janela de rastreamento.  
|**Para baixo**|Depois de selecionar uma coluna de dados, clique em **Para Baixo** para mover as colunas de dados para fora de **Grupos**. Você também pode clicar em **Abaixo** para reorganizar a exibição de colunas na janela de rastreamento.  
## <a name="edit-filter"></a>Editar filtro
Use a caixa de diálogo **Editar Filtro** para criar e modificar filtros da coluna de dados em um rastreamento. Clique em um nome de coluna na lista para exibir os critérios de filtro disponíveis para essa coluna de dados no painel adjacente. Insira os critérios de filtro e clique em **OK** para aplicá-los à coluna de dados selecionada. Se aparecer um ícone de filtro à esquerda do nome da coluna de dados, isso significa que essa coluna já tem um filtro configurado.  
 >[!NOTE]
 >Para colunas de dados do tipo cadeia de caracteres, os critérios de filtro exibirão um valor de cadeia de caracteres LIKE ou NOT LIKE.  

## <a name="select-template-name"></a>Selecionar Nome do Modelo
Use a caixa de diálogo **Selecionar Nome do Modelo** para selecionar um modelo de rastreamento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] existente para exportar para um arquivo no sistema operacional. Você também pode usar essa caixa de diálogo para selecionar ou digitar um nome diferente a fim de salvar um modelo de rastreamento ao editar um modelo de rastreamento existente. Para acessar essa caixa de diálogo ao exportar um modelo, no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu, point to **Templates**, and then click **Export Template**. Para acessar essa caixa de diálogo ao mudar o nome de um modelo, no menu **Arquivo** , aponte para **Modelos**, aponte para **Editar Modelo**e, então, clique em **Salvar Como**.  
|Item|Description
|---|---
|**Tipo de servidor**|Selecione o tipo de servidor do qual você quer escolher um modelo. Essa opção só está disponível quando você estiver exportando um modelo.  
|**Nome do modelo**|Digite um nome de modelo novo ou selecione um nome de modelo da lista. Se estiver exportando um modelo, você poderá selecionar somente um nome de modelo da lista. 

## <a name="see-also"></a>Confira também 
[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
[Monitoramento de desempenho e atividade de servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)  
  
  
