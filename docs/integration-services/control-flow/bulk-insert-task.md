---
title: Tarefa Bulk Insert | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.bulkinserttask.f1
- sql13.dts.designer.bulkinserttask.connection.f1
- sql13.dts.designer.bulkinserttask.general.f1
- sql13.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 72f40019acada98168cf425dca983154e0e2dc8f
ms.contentlocale: pt-br
ms.lasthandoff: 08/11/2017

---
# <a name="bulk-insert-task"></a>Tarefa Inserção em Massa
  A tarefa Inserção em Massa fornece uma maneira eficiente de copiar grandes volumes de dados em uma tabela ou exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, suponha que a empresa armazena sua lista de produtos em milhões de linhas em um sistema de mainframe, mas o sistema de comércio eletrônico da empresa usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para preencher páginas da Web. Você deve atualizar a tabela de produtos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todas as noites com a lista principal de produtos do mainframe. Para atualizar a tabela, você salva a lista de produtos em um formato delimitado por guia e usa a tarefa de inserção em massa para copiar os dados diretamente na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para assegurar a cópia de dados em alta velocidade, não podem ser executadas transformações nos dados enquanto estiver transferindo do arquivo de origem à tabela ou exibição.  
  
## <a name="usage-considerations"></a>Considerações de uso  
 Antes de utilizar a tarefa de inserção em massa, considere o seguinte:  
  
-   A tarefa de Inserção em massa só pode transferir dados de um arquivo de texto em uma tabela ou de exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para utilizar a tarefa de inserção em massa para transferir dados de outros sistemas de gerenciamento de bancos de dados (DBMSs), você deve exportar os dados da fonte para um arquivo de texto e então importar os dados do arquivo de texto para uma tabela ou exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O destino deve ser uma tabela ou exibição em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se a tabela ou exibição de destino já contém dados, os novos dados são anexados aos dados existentes quando a tarefa de inserção em massa é executada. Se você quiser substituir os dados, execute uma tarefa Execute SQL que executa uma instrução de DELETE ou TRUNCATE antes de você executar a tarefa de Inserção em massa . Para obter mais informações, consulte [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md).  
  
-   Você pode usar um arquivo de formato no objeto de tarefa da inserção em massa . Se você tiver um arquivo de formato que foi criado pelo utilitário do **bcp** , você poderá especificar seu caminho na tarefa de inserção em massa . A tarefa de inserção em massa fornece suporte tanto para arquivos em formato XML quanto não XML. Para obter mais informações sobre os arquivos de formato, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Somente membros da função de servidor fixa sysadmin podem executar um pacote que contenha uma tarefa Inserção em Massa.  
  
## <a name="bulk-insert-task-with-transactions"></a>Tarefa Inserção em Massa com Transações  
 Se um tamanho de lote não for definido, toda a operação de cópia em massa é tratada como uma transação. Um tamanho de lote de **0** indica que os dados são inseridos em um lote. Se um tamanho de lote for definido, cada lote representa uma transação que é confirmada quando o lote terminar de ser executado.  
  
 O comportamento da tarefa de inserção em massa , à medida que se relaciona com as transações, leva em conta se a tarefa une a transação de pacotes. Se a tarefa de inserção em massa não unir a transação de pacotes, cada lote sem-erros está confirmado como uma unidade antes que o próximo lote seja tentado. Se a tarefa de inserção em massa unir a transação de pacotes, lotes sem-erros permanecem na transação na conclusão da tarefa. Esses lotes estão sujeitos à confirmação ou operação de reversão do pacote.  
  
 Uma falha na tarefa de inserção em massa não reverte automaticamente com êxito os lotes carregados, assim como, se a tarefa tiver êxito, os lotes não serão confirmados automaticamente. As operações de confirmação e reversão ocorrem apenas em resposta ao pacote e às configurações de propriedade de fluxo de trabalho.  
  
## <a name="source-and-destination"></a>Origem e destino  
 Quando você especificar o local do arquivo de origem de texto, considere o seguinte:  
  
-   O servidor deve ter permissão para acessar tanto o arquivo quanto o banco de dados de destino.  
  
-   O servidor executa a tarefa de inserção em massa . Então, qualquer arquivo de formato que a tarefa utilize deve estar localizado no servidor.  
  
-   O arquivo de origem que a tarefa de inserção em massa carregar pode estar no mesmo servidor que o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual são inseridos os dados, ou em um servidor remoto. Se o arquivo estiver em um servidor remoto, você deve especificar o nome de arquivo usando o nome UNC no caminho.  
  
## <a name="performance-optimization"></a>Otimização do desempenho  
 Para aperfeiçoar o desempenho, considere o seguinte:  
  
-   Se o arquivo de texto estiver alocado no mesmo computador que a base de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual estão inseridos os dados, a operação de cópia ocorre a uma taxa ainda mais rápida, porque os dados não são movidos pela rede.  
  
-   A tarefa de inserção em massa não registra linhas que causam erro. Se você precisa capturar essas informações, use as saídas de erro de componentes de fluxo de dados para capturar linhas que causam erro em um arquivo de exceção.  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>Entradas de log personalizado disponíveis na tarefa de inserção em massa  
 A seguinte tabela relaciona as entradas de log personalizadas para a tarefa inserção em massa . Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**BulkInsertTaskBegin**|Indica que a inserção em massa iniciou.|  
|**BulkInsertTaskEnd**|Indica que a inserção em massa foi concluída.|  
|**BulkInsertTaskInfos**|Fornece informações descritivas sobre a tarefa.|  
  
## <a name="bulk-insert-task-configuration"></a>Configuração da tarefa Inserção em Massa  
 Você pode configurar a tarefa de inserção em massa das seguintes maneiras:  
  
-   Especifique o gerenciador de conexões do OLE DB para conectar-se ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e à tabela ou exibição nos quais estão inseridos os dados. A tarefa de inserção em massa aceita apenas conexões do OLE DB para o banco de dados de destino.  
  
-   Especifique o gerenciador de conexões do Arquivo ou Arquivo Simples para acessar o arquivo de origem. A tarefa de inserção em massa usa o gerenciador de conexões apenas para o local do arquivo de origem. A tarefa ignora outras opções que você selecionar no editor do gerenciador de conexões.  
  
-   Defina o formato que é usado pela tarefa de inserção em massa que usa um arquivo de formato ou, definindo os delimitadores de coluna e fila dos dados de origem. Se estiver usando um arquivo de formato, especifique o gerenciador de conexões do Arquivo para acessar o arquivo de formato.  
  
-   Especifique as ações para realizar na tabela de destino ou de exibição quando a tarefa inserir os dados. As opções incluem se devemos verificar restrições, habilitar inserções de identidade, manter nulos, acionar gatilhos ou fechar a tabela.  
  
-   Forneça informações sobre o lote de dados a inserir, tais como o tamanho do lote, a primeira e a última linha do arquivo a inserir, o número de erros de inserção que podem acontecer antes que a tarefa pare de inserir linhas e os nomes das colunas que serão ordenadas.  
  
 Se a tarefa de inserção em massa usar um gerenciador de conexões do Arquivo Simples para acessar o arquivo de origem, a tarefa não usa o formato especificado no gerenciador de conexões do Arquivo Simples. Em vez disso, a tarefa de Inserção em massa usa o formato especificado em um arquivo de formato ou os valores das propriedades RowDelimiter e ColumnDelimiter da tarefa.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>Configuração programática da tarefa Inserção em Massa  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico, [You may get "Unable to prepare the SSIS bulk insert for data insertion" error on UAC enabled systems](http://go.microsoft.com/fwlink/?LinkId=233693), em support.microsoft.com.  
  
-   Artigo técnico, [The Data Loading Performance Guide](http://go.microsoft.com/fwlink/?LinkId=233700), em msdn.microsoft.com.  
  
-   Artigo técnico, [Using SQL Server Integration Services to Bulk Load Data](http://go.microsoft.com/fwlink/?LinkId=233701)(Usando o SQL Server Integration Services para carregar dados em massa), em simple-talk.com.  
  
## <a name="bulk-insert-task-editor-connection-page"></a>Editor da Tarefa Inserção em Massa (página Conexão)
  Use a página **Conexão** da caixa de diálogo **Editor da Tarefa Inserção em Massa** para especificar a origem e o destino da operação de inserção em massa e o formato a ser usado.  
  
 Para saber mais sobre como trabalhar com inserções em massa, consulte [Tarefa Inserção em Massa](../../integration-services/control-flow/bulk-insert-task.md) e [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
### <a name="options"></a>Opções  
 **Conexão**  
 Selecione um Gerenciador de conexão OLE DB na lista ou clique em \< **nova conexão...** > para criar uma nova conexão.  
  
 **Tópicos relacionados:** [Gerenciador de Conexão do OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
 **Tabela de Destino**  
 Digite o nome da tabela ou exibição de destino ou selecione uma tabela ou exibição na lista.  
  
 **Formato**  
 Selecione a fonte do formato para a inserção em massa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Usar Arquivo**|Selecione um arquivo que contém a especificação de formato. Selecionar esta opção faz com que seja exibida a opção dinâmica **Arquivo de Formato**.|  
|**Especificar**|Especifique o formato. Selecionar esta opção faz com que sejam exibidas as opções dinâmicas **RowDelimiter** e **ColumnDelimiter**.|  
  
 **Arquivo**  
 Selecione um Gerenciador de conexão de arquivo ou arquivo simples na lista ou clique em \< **nova conexão...** > para criar uma nova conexão.  
  
 O local do arquivo está relacionado ao Mecanismo de Banco de Dados do SQL Server especificado no gerenciador de conexões para esta tarefa. O arquivo de texto deve ser acessível pelo Mecanismo de Banco de Dados do SQL Server em um disco rígido local no servidor, por um compartilhamento ou unidade mapeada para o SQL Server. O arquivo não pode ser acessado pelo Tempo de Execução do SSIS.  
  
 Se você acessa o arquivo de origem usando um gerenciador de conexões de Arquivo Simples, a tarefa de Inserção em Massa não usa o formato especificado no gerenciador de conexões de Arquivos Simples. Em vez disso, a tarefa de Inserção em massa usa o formato especificado em um arquivo de formato ou os valores das propriedades RowDelimiter e ColumnDelimiter da tarefa.  
  
 **Tópicos relacionados:** [Gerenciador de Conexão de arquivo](../../integration-services/connection-manager/file-connection-manager.md), [simples Gerenciador de Conexão de arquivo](../../integration-services/connection-manager/flat-file-connection-manager.md) 
  
 **Atualizar Tabelas**  
 Atualize a lista de tabelas e exibições.  
  
### <a name="format-dynamic-options"></a>Opções Dinâmicas de Formato  
  
#### <a name="format--use-file"></a>Formato = Usar Arquivo  
 **Arquivo de Formato**  
 Digite o caminho do arquivo de formato ou clique no botão de reticências **(…)** para localizar o arquivo.  
  
#### <a name="format--specify"></a>Formato = Especificar  
 **RowDelimiter**  
 Especifique o delimitador de linhas no arquivo de origem. O valor padrão é **{CR}{LF}**.  
  
 **ColumnDelimiter**  
 Especifique o delimitador de colunas no arquivo de origem. O padrão é **Tab**.  
  
## <a name="bulk-insert-task-editor-general-page"></a>Editor da Tarefa Inserção em Massa (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Inserção em Massa** para nomear e descrever a tarefa Inserção em Massa.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Inserção em Massa. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição para a tarefa Inserção em Massa.  
 
## <a name="bulk-insert-task-editor-options-page"></a>Editor da Tarefa Inserção em Massa (página de Opções)
  Use a página **Opções** da caixa de diálogo **Editor da Tarefa Inserção em Massa** para definir as propriedades da operação de inserção em massa. A tarefa Inserção em Massa copia uma grande quantidade de dados em uma exibição ou tabela do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para saber mais sobre como trabalhar com inserções em massa, consulte [Tarefa Inserção em Massa](../../integration-services/control-flow/bulk-insert-task.md) e [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
### <a name="options"></a>Opções  
 **CodePage**  
 Especifique a página de código dos dados no arquivo de dados.  
  
 **DataFileType**  
 Especifique o valor do tipo de dados a ser usado na operação de carregamento.  
  
 **BatchSize**  
 Especifique o número de linhas em um lote. O padrão é todo o arquivo de dados. Se você definir **BatchSize** para zero, os dados serão carregados em um único lote.  
  
 **LastRow**  
 Especifique a última linha a ser copiada.  
  
 **FirstRow**  
 Especifique a primeira linha da qual começar a copiar.  
  
 **Opções**  
 |Termo|Definição|  
|----------|----------------|  
|**Verificar restrições**|Selecione para verificar as restrições de tabelas e colunas.|  
|**Manter nulos**|Selecione para reter valores nulos durante a operação de inserção em massa, em vez de inserir qualquer valor padrão para colunas vazias.|  
|**Habilitar inserção de identidade**|Selecione para inserir valores existentes em uma coluna de identidade.|  
|**Bloqueio de tabela**|Selecione para bloquear a tabela durante a inserção em massa.|  
|**Acionadores**|Selecione para acionar qualquer inserção, atualização ou exclusão de gatilhos na tabela.|  
  
 **SortedData**  
 Especifique a cláusula ORDER BY na instrução de inserção em massa. O nome da coluna que você fornece deve ser uma coluna válida na tabela de destino. O padrão é **false**. Isto significa que os dados não são classificados por uma cláusula ORDER BY.  
  
 **MaxErrors**  
 Especifique o número máximo de erros que podem ocorrer antes que a operação de inserção em massa seja cancelada. Um valor de 0 indica que um número infinito de erros é permitido.  
  
> [!NOTE]  
>  Cada linha que não pode ser importada pela operação de carregamento em massa é contada como um erro.  
  

