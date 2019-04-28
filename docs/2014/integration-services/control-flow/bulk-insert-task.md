---
title: Tarefa Inserção em Massa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9b5da9ff28dc658f870033a02fe88b14ea442c51
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832868"
---
# <a name="bulk-insert-task"></a>Tarefa Inserção em Massa
  A tarefa Inserção em Massa fornece uma maneira eficiente de copiar grandes volumes de dados em uma tabela ou exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, suponha que a empresa armazena sua lista de produtos em milhões de linhas em um sistema de mainframe, mas o sistema de comércio eletrônico da empresa usa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para preencher páginas da Web. Você deve atualizar a tabela de produtos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todas as noites com a lista principal de produtos do mainframe. Para atualizar a tabela, você salva a lista de produtos em um formato delimitado por guia e usa a tarefa de inserção em massa para copiar os dados diretamente na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para assegurar a cópia de dados em alta velocidade, não podem ser executadas transformações nos dados enquanto estiver transferindo do arquivo de origem à tabela ou exibição.  
  
## <a name="usage-considerations"></a>Considerações de uso  
 Antes de utilizar a tarefa de inserção em massa, considere o seguinte:  
  
-   A tarefa de Inserção em massa só pode transferir dados de um arquivo de texto em uma tabela ou de exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para utilizar a tarefa de inserção em massa para transferir dados de outros sistemas de gerenciamento de bancos de dados (DBMSs), você deve exportar os dados da fonte para um arquivo de texto e então importar os dados do arquivo de texto para uma tabela ou exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O destino deve ser uma tabela ou exibição em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se a tabela ou exibição de destino já contém dados, os novos dados são anexados aos dados existentes quando a tarefa de inserção em massa é executada. Se você quiser substituir os dados, execute uma tarefa Execute SQL que executa uma instrução de DELETE ou TRUNCATE antes de você executar a tarefa de Inserção em massa . Para obter mais informações, consulte [Execute SQL Task](execute-sql-task.md).  
  
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
 A seguinte tabela relaciona as entradas de log personalizadas para a tarefa inserção em massa . Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../custom-messages-for-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`BulkInsertTaskBegin`|Indica que a inserção em massa iniciou.|  
|`BulkInsertTaskEnd`|Indica que a inserção em massa foi concluída.|  
|`BulkInsertTaskInfos`|Fornece informações descritivas sobre a tarefa.|  
  
## <a name="bulk-insert-task-configuration"></a>Configuração da tarefa Inserção em Massa  
 Você pode configurar a tarefa de inserção em massa das seguintes maneiras:  
  
-   Especifique o gerenciador de conexões do OLE DB para conectar-se ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e à tabela ou exibição nos quais estão inseridos os dados. A tarefa de inserção em massa aceita apenas conexões do OLE DB para o banco de dados de destino.  
  
-   Especifique o gerenciador de conexões do Arquivo ou Arquivo Simples para acessar o arquivo de origem. A tarefa de inserção em massa usa o gerenciador de conexões apenas para o local do arquivo de origem. A tarefa ignora outras opções que você selecionar no editor do gerenciador de conexões.  
  
-   Defina o formato que é usado pela tarefa de inserção em massa que usa um arquivo de formato ou, definindo os delimitadores de coluna e fila dos dados de origem. Se estiver usando um arquivo de formato, especifique o gerenciador de conexões do Arquivo para acessar o arquivo de formato.  
  
-   Especifique as ações para realizar na tabela de destino ou de exibição quando a tarefa inserir os dados. As opções incluem se devemos verificar restrições, habilitar inserções de identidade, manter nulos, acionar gatilhos ou fechar a tabela.  
  
-   Forneça informações sobre o lote de dados a inserir, tais como o tamanho do lote, a primeira e a última linha do arquivo a inserir, o número de erros de inserção que podem acontecer antes que a tarefa pare de inserir linhas e os nomes das colunas que serão ordenadas.  
  
 Se a tarefa de inserção em massa usar um gerenciador de conexões do Arquivo Simples para acessar o arquivo de origem, a tarefa não usa o formato especificado no gerenciador de conexões do Arquivo Simples. Em vez disso, a tarefa de Inserção em massa usa o formato especificado em um arquivo de formato ou os valores das propriedades RowDelimiter e ColumnDelimiter da tarefa.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Inserção em Massa &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor da Tarefa Inserção em Massa &#40;Página Conexão&#41;](../bulk-insert-task-editor-connection-page.md)  
  
-   [Editor da Tarefa Inserção em Massa &#40;Página Opções&#41;](../bulk-insert-task-editor-options-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>Configuração programática da tarefa Inserção em Massa  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico, [You may get "Unable to prepare the SSIS bulk insert for data insertion" error on UAC enabled systems](https://go.microsoft.com/fwlink/?LinkId=233693)(Você pode receber o erro “Não é possível preparar a inserção em massa do SSIS para a inserção de dados” em sistemas habilitados para UAC), em support.microsoft.com.  
  
-   Artigo técnico, [The Data Loading Performance Guide](https://go.microsoft.com/fwlink/?LinkId=233700), em msdn.microsoft.com.  
  
-   Artigo técnico, [Using SQL Server Integration Services to Bulk Load Data](https://go.microsoft.com/fwlink/?LinkId=233701)(Usando o SQL Server Integration Services para carregar dados em massa), em simple-talk.com.  
  
  
