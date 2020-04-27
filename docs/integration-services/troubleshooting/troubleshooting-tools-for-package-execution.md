---
title: Ferramentas de solução de problemas para execução de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c8142eaf9628d873819c2cebbac79da0d23787a3
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086845"
---
# <a name="troubleshooting-tools-for-package-execution"></a>Solucionando problemas de ferramentas para execução de pacotes

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui recursos e ferramentas que podem ser usados para solucionar problemas de pacotes quando eles são executados depois de concluídos e implantados.  
  
 No momento da criação, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece pontos de interrupção para pausar a execução do pacote, a janela Progresso, e os visualizadores de dados para visualizar como os dados passam pelo fluxo de dados. No entanto, esses recursos não estarão disponíveis quando você estiver executando pacotes que foram implantados. As principais técnicas para a solução problemas de pacotes implantados são as seguintes:  
  
-   Capturar e manipular os erros de pacote usando os manipuladores de eventos.  
  
-   Capturar dados inválidos usando saídas de erro.  
  
-   Controlar as etapas de execução do pacote usando os logs.  
  
 Você também pode usar as seguintes dicas e técnicas para evitar problemas ao executar os pacotes.  
  
-   **Ajudar a garantir a integridade dos dados usando as transações**. Para obter mais informações, consulte [Transações do Integration Services](../../integration-services/integration-services-transactions.md).  
  
-   **Reiniciar os pacotes a partir do ponto de falha usando os pontos de verificação**. Para saber mais, confira [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>Capturar e manipular os erros de pacotes com os manipuladores de eventos  
 Você pode responder a muitos eventos gerados pelo pacote e os objetos no pacote usando os manipuladores de eventos.  
  
-   **Criar um manipulador de eventos para o evento OnError**. No manipulador de eventos, você pode usar uma tarefa Enviar Email para notificar um administrador sobre a falha, usar uma tarefa Script e a lógica personalizada para obter informações do sistema para a solução de problemas, ou limpar os recursos temporários ou as saídas incompletas. Para obter mais informações, consulte [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md).  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>Solucionar problemas de dados inválidos por meio das saídas de erro  
 Você pode usar a saída de erro disponível em muitos componentes de fluxo de dados para direcionar as linhas com erros a outro destino para análise posterior. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).  
  
-   **Capturar dados inválidos usando saídas de erro**. Envie as linhas que contêm erros a outro destino como uma tabela de erros ou um arquivo de texto. A saída de erro adiciona linhas automaticamente a duas colunas que contém o número do erro que fez com que a linha fosse rejeitada e a ID da coluna na qual o erro ocorreu.  
  
-   **Adicionar informações amigáveis às saídas de erro**. A análise da saída de erro pode tornar-se uma tarefa mais fácil se você adicionar a mensagem de erro e o nome da coluna além dos dois identificadores numéricos que são fornecidos pela saída de erro. Para obter um exemplo de como acrescentar essas duas colunas adicionais usando scripts, consulte [Aprimorando uma saída de erro com o componente Script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
-   **Ou obtenha os nomes de coluna registrando o evento DiagnosticEx**. Esse evento grava um mapa de linhagem de fluxo de dados no log. Em seguida, você pode procurar o nome da coluna nesse mapa de linhagem usando o identificador da coluna capturado por uma saída do erro.  Para obter mais informações, consulte [Tratamento de erro em dados](../../integration-services/data-flow/error-handling-in-data.md).  
  
     O valor da coluna de mensagem para **DiagnosticEx** é texto XML. Para exibir o texto da mensagem para uma execução de pacote, consulte a exibição [catalog.operation_messages &#40;Banco de Dados SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md). Observe que o evento **DiagnosticEx** não preservar o espaço em branco em sua saída XML, a fim de reduzir o tamanho do log. Para melhorar a legibilidade, copie o log em um editor de XML, no Visual Studio, por exemplo, que ofereça suporte à formatação XML e ao realce de sintaxe.  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>Solucionar problemas de execução de pacotes por meio relatórios de operações  
 Os relatórios de operações padrão estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ajudar você a monitorar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram implantados no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses relatórios de pacote ajudam a exibir o status e o histórico do pacote e, se necessário, a identificar a causa de falhas de execução.  
  
 Para obter mais informações, consulte [Solucionando problemas de relatórios para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-reports-for-package-execution.md).  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>Solucionar problemas de execução de pacotes usando exibições SSISDB  
 Várias exibições de banco de dados SSISDB estão disponíveis para você consultar e monitorar a execução de pacotes e outras informações de operações. Para obter mais informações, consulte [Monitorar a execução de pacotes e outras operações](../../integration-services/performance/monitor-running-packages-and-other-operations.md).  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>Solucionar problemas de execução de pacotes por meio dos logs  
 Você pode controlar muitas ocorrências em seus pacotes de execução ativando os logs. Os provedores de logs capturam as informações sobre os eventos especificados para análise posterior e salvam essas informações em uma tabela de banco de dados, um arquivo simples, um arquivo XML ou outro formato de saída suportado.  
  
-   **Habilitar logs**. Você pode refinar a saída de logs selecionando apenas os eventos e apenas os itens de informação que deseja capturar. Para obter mais informações, consulte [Log do SSIS (Integration Services)](../performance/integration-services-ssis-logging.md).  
  
-   **Selecione o evento de Diagnóstico do pacote para solucionar problemas do provedor.** Existem mensagens de log que ajudam a solucionar os problemas de interação do pacote com as fontes de dados externas. Para obter mais informações, consulte [Solução de problemas de conectividade de pacotes de ferramentas](troubleshooting-tools-for-package-connectivity.md).  
  
-   **Aprimorar a saída de log padrão**. Normalmente, o log acrescenta linhas ao destino de log sempre que um pacote é executado. Embora cada linha de saída do log identifique o pacote de acordo com seu nome e identificador exclusivos, além de identificar também a execução do pacote por um ExecutionID exclusivo, uma quantidade muito grande de saídas de logs em uma lista simples pode dificultar a análise.  
  
     A abordagem a seguir é uma sugestão para aprimorar a saída de log padrão e facilitar a geração de relatórios:  
  
    1.  **Criar uma tabela pai que registra todas as execuções de um pacote**. Essa tabela pai tem apenas uma linha para cada execução do pacote e usa o ExecutionID para estabelecer um vínculo com os registros filho na tabela de log [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Você pode usar uma tarefa Executar SQL no início de cada pacote para criar essa nova linha e para registrar a hora de início. Em seguida, poderá usar outra tarefa Executar SQL no final do pacote para atualizar a linha com a hora de término, a duração e o status.  
  
    2.  **Adicionar informações de auditoria ao fluxo de dados**. Você pode usar a transformação Auditoria para adicionar informações às linhas no fluxo de dados sobre a execução do pacote que criou ou modificou cada linha. A transformação Auditoria disponibiliza nove partes de informações, incluindo PackageName e ExecutionInstanceGUID. Para obter mais informações, consulte [Audit Transformation](../../integration-services/data-flow/transformations/audit-transformation.md). Se você tiver informações personalizadas que gostaria de incluir nas linhas para fins de auditoria, poderá adicioná-las às linhas no fluxo de dados usando uma transformação Coluna Derivada. Para obter mais informações, consulte [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
    3.  **Considerar a captura de dados de contagem de linhas**. Considere a criação de tabelas separadas para as informações de contagem de linhas, onde cada instância de execução de pacote possa ser identificada por ExecutionID. Use a transformação Contagem de Linhas para salvar a contagem de linhas em uma série de variáveis em pontos críticos no fluxo de dados. Após o término do fluxo de dados, use uma tarefa Executar SQL para inserir as séries de valores em uma linha na tabela para análise e geração de relatório posterior.  
  
     Para obter mais informações sobre essa abordagem, consulte a seção "ETL Auditing and Logging" no white paper da [!INCLUDE[msCoName](../../includes/msconame-md.md)] intitulado [Projeto REAL: práticas de design ETL de Business Intelligence](https://www.microsoft.com/download/details.aspx?id=14582).  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>Solucionar problemas de execução de pacotes por meio de arquivos de despejo de depuração  
 No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode criar arquivos de despejo de depuração que fornecem informações sobre a execução de um pacote. Para obter mais informações, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
## <a name="troubleshoot-run-time-validation-issues"></a>Solucionar problemas de validação em tempo de execução  
 Às vezes, você não poderá se conectar às suas fontes de dados ou validar partes de seu pacote até que as tarefas anteriores no pacote tenham sido executadas. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os seguintes recursos para ajudar a evitar os erros de validação que resultam dessas condições:  
  
-   **Configurar uma propriedade DelayValidation em elementos de pacote que não são válidos quando o pacote estiver carregado**. Você pode definir **DelayValidation** para **True** em elementos do pacote cujas configurações não são válidas para evitar erros de validação quando o pacote for carregado. Por exemplo, você pode ter uma tarefa Fluxo de Dados que usa uma tabela de destino que não existe até que uma tarefa Executar SQL crie a tabela no tempo de execução. A propriedade **DelayValidation** pode ativada no nível do pacote ou no nível das tarefas individuais e contêineres que o pacote inclui.  
  
     A propriedade **DelayValidation** pode ser definida em uma tarefa de Fluxo de Dados, mas não em componentes de fluxo de dados individuais. Você pode conseguir um efeito semelhante definindo a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> dos componentes de fluxo de dados individuais como **false**. Entretanto, quando o valor dessa propriedade for **false**, o componente não reconhecerá as alterações para o metadados de fontes de dados externas. Ao definir como **true**, a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> poderá ajudar a evitar os problemas de bloqueio causados por bloqueios no banco de dados, especialmente quando o pacote estiver usando as transações.  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>Solucionar problemas de permissões em tempo de execução  
 Se você encontrar erros ao tentar executar os pacotes implantados usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, as contas usadas pelo Agent poderão não ter as permissões necessárias. Para obter informações sobre como solucionar problemas de pacotes executados nos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Um pacote SSIS não é executado ao chamar o pacote SSIS a partir de uma etapa de trabalho do SQL Server Agent](https://support.microsoft.com/kb/918760). Para obter mais informações sobre como executar pacotes por meio de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Trabalhos do SQL Server Agent para pacotes](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).  
  
 Para se conectar a fontes de dados do Excel ou do Access, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent requer uma conta com permissão para ler, gravar, criar e excluir arquivos temporários na pasta especificada pelas variáveis de ambiente TEMP e TMP.  
  
## <a name="troubleshoot-64-bit-issues"></a>Solucionar problemas de 64 bits  
  
-   **Alguns provedores de dados não estão disponíveis em plataformas de 64 bits**. Em particular, o Provedor OLE DB do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet, que é necessário para conectar as fontes de dados do Excel ou do Access, não está disponível em versões de 64 bits.  
  
## <a name="troubleshoot-errors-without-a-description"></a>Solucionar problemas de erros sem uma descrição  
 Se você encontrar um erro do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que não seja acompanhado de uma descrição, localize a descrição no [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md) e procure o erro pelo número. No momento, a lista não inclui informações para solução de problemas.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurar o fluxo de dados](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
