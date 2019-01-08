---
title: Ferramentas de solução de problemas para execução de pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca170bbae969db8610e1e0ec6e61e3e68fa905f4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377628"
---
# <a name="troubleshooting-tools-for-package-execution"></a>Solucionando problemas de ferramentas para execução de pacotes
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui recursos e ferramentas que podem ser usados para solucionar problemas de pacotes quando eles são executados depois de concluídos e implantados.  
  
 No momento da criação, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] fornece pontos de interrupção para pausar a execução do pacote, a janela Progresso, e os visualizadores de dados para visualizar como os dados passam pelo fluxo de dados. No entanto, esses recursos não estarão disponíveis quando você estiver executando pacotes que foram implantados. As principais técnicas para a solução problemas de pacotes implantados são as seguintes:  
  
-   Capturar e manipular os erros de pacote usando os manipuladores de eventos.  
  
-   Capturar dados inválidos usando saídas de erro.  
  
-   Controlar as etapas de execução do pacote usando os logs.  
  
 Você também pode usar as seguintes dicas e técnicas para evitar problemas ao executar os pacotes.  
  
-   **Ajudar a garantir a integridade dos dados usando as transações**. Para obter mais informações, consulte [Transações do Integration Services](../integration-services-transactions.md).  
  
-   **Reiniciar os pacotes a partir do ponto de falha usando os pontos de verificação**. Para saber mais, confira [Reiniciar pacotes por meio de pontos de verificação](../packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>Capturar e manipular os erros de pacotes com os manipuladores de eventos  
 Você pode responder a muitos eventos gerados pelo pacote e os objetos no pacote usando os manipuladores de eventos.  
  
-   **Criar um manipulador de eventos para o evento OnError**. No manipulador de eventos, você pode usar uma tarefa Enviar Email para notificar um administrador sobre a falha, usar uma tarefa Script e a lógica personalizada para obter informações do sistema para a solução de problemas, ou limpar os recursos temporários ou as saídas incompletas. Para obter mais informações, consulte [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../integration-services-ssis-event-handlers.md).  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>Solucionar problemas de dados inválidos por meio das saídas de erro  
 Você pode usar a saída de erro disponível em muitos componentes de fluxo de dados para direcionar as linhas com erros a outro destino para análise posterior.  
  
-   **Capturar dados inválidos usando saídas de erro**. Envie as linhas que contêm erros a outro destino como uma tabela de erros ou um arquivo de texto. A saída de erro adiciona linhas automaticamente a duas colunas que contém o número do erro que fez com que a linha fosse rejeitada e a ID da coluna na qual o erro ocorreu. Para obter mais informações, consulte [Tratamento de erros em dados](../data-flow/error-handling-in-data.md).  
  
-   **Adicionar informações amigáveis às saídas de erro**. A análise da saída de erro pode tornar-se uma tarefa mais fácil se você adicionar outras informações descritivas além dos dois identificadores numéricos que são fornecidos pela saída de erro.  
  
     **Adicionar a descrição do erro**. É fácil procurar pela descrição do erro usando um componente Script. Para obter mais informações, consulte [aprimorando uma saída de erro para o componente Script](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
     **Adicione o nome da coluna de erro**. A pesquisa pelo nome de coluna que corresponde à ID da coluna salva pela saída de erro não pode ser feita facilmente no componente Script e requer etapas adicionais. Cada ID de coluna em um fluxo de dados é exclusivo dentro da tarefa Fluxo de Dados e persiste no pacote no momento da criação. A abordagem a seguir é uma sugestão para adicionar o nome de coluna à saída do erro. Para obter um exemplo de como usar essa abordagem, consulte [adicionando o nome de coluna de erro para uma saída de erro](https://go.microsoft.com/fwlink/?LinkId=261546) em dougbert.com.  
  
    1.  **Criar uma tabela de pesquisa de nomes de coluna**. Crie outro aplicativo separado que use a API do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para iterar com cada pacote salvo, cada fluxo do pacote, cada objeto do fluxo de dados, e cada entrada e saída do objeto de fluxo de dados. O aplicativo deve persistir a ID de coluna e o nome de cada coluna a uma tabela de pesquisa, com a ID da tarefa Fluxo de Dados pai e a ID do pacote.  
  
    2.  **Adicionar o nome da coluna à saída**. Adicione uma transformação Pesquisa à saída de erro que pesquise pelo nome da coluna na tabela de pesquisa criada na etapa anterior. A pesquisa pode usar a ID da coluna na saída de erro, a ID do pacote (disponível na variável System::PackageID do sistema) e a ID da tarefa Fluxo de Dados (disponível na variável System::TaskID do sistema).  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>Solucionar problemas de execução de pacotes por meio relatórios de operações  
 Os relatórios de operações padrão estão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ajudar você a monitorar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foram implantados no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses relatórios de pacote ajudam a exibir o status e o histórico do pacote e, se necessário, a identificar a causa de falhas de execução.  
  
 Para obter mais informações, consulte [Solucionando problemas de relatórios para execução de pacotes](troubleshooting-reports-for-package-execution.md).  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>Solucionar problemas de execução de pacotes usando exibições SSISDB  
 Várias exibições de banco de dados SSISDB estão disponíveis para você consultar e monitorar a execução de pacotes e outras informações de operações. Para obter mais informações, consulte [monitoramento para execuções de pacote e outras operações](../performance/monitor-running-packages-and-other-operations.md).  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>Solucionar problemas de execução de pacotes por meio dos logs  
 Você pode controlar muitas ocorrências em seus pacotes de execução ativando os logs. Os provedores de logs capturam as informações sobre os eventos especificados para análise posterior e salvam essas informações em uma tabela de banco de dados, um arquivo simples, um arquivo XML ou outro formato de saída suportado.  
  
-   **Habilitar logs**. Você pode refinar a saída de logs selecionando apenas os eventos e apenas os itens de informação que deseja capturar. Para obter mais informações, consulte [Registro em Log do Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Registro em Log do Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md).  
  
-   **Selecione o evento de Diagnóstico do pacote para solucionar problemas do provedor.** Existem mensagens de log que ajudam a solucionar os problemas de interação do pacote com as fontes de dados externas. Para obter mais informações, consulte [Solução de problemas de conectividade de pacotes de ferramentas](troubleshooting-tools-for-package-connectivity.md).  
  
-   **Aprimorar a saída de log padrão**. Normalmente, o log acrescenta linhas ao destino de log sempre que um pacote é executado. Embora cada linha de saída do log identifique o pacote de acordo com seu nome e identificador exclusivos, além de identificar também a execução do pacote por um ExecutionID exclusivo, uma quantidade muito grande de saídas de logs em uma lista simples pode dificultar a análise.  
  
     A abordagem a seguir é uma sugestão para aprimorar a saída de log padrão e facilitar a geração de relatórios:  
  
    1.  **Criar uma tabela pai que registra todas as execuções de um pacote**. Essa tabela pai tem apenas uma linha para cada execução do pacote e usa o ExecutionID para estabelecer um vínculo com os registros filho na tabela de log [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Você pode usar uma tarefa Executar SQL no início de cada pacote para criar essa nova linha e para registrar a hora de início. Em seguida, poderá usar outra tarefa Executar SQL no final do pacote para atualizar a linha com a hora de término, a duração e o status.  
  
    2.  **Adicionar informações de auditoria ao fluxo de dados**. Você pode usar a transformação Auditoria para adicionar informações às linhas no fluxo de dados sobre a execução do pacote que criou ou modificou cada linha. A transformação Auditoria disponibiliza nove partes de informações, incluindo PackageName e ExecutionInstanceGUID. Para obter mais informações, consulte [Audit Transformation](../data-flow/transformations/audit-transformation.md). Se você tiver informações personalizadas que gostaria de incluir nas linhas para fins de auditoria, poderá adicioná-las às linhas no fluxo de dados usando uma transformação Coluna Derivada. Para obter mais informações, consulte [Derived Column Transformation](../data-flow/transformations/derived-column-transformation.md).  
  
    3.  **Considerar a captura de dados de contagem de linhas**. Considere a criação de tabelas separadas para as informações de contagem de linhas, onde cada instância de execução de pacote possa ser identificada por ExecutionID. Use a transformação Contagem de Linhas para salvar a contagem de linhas em uma série de variáveis em pontos críticos no fluxo de dados. Após o término do fluxo de dados, use uma tarefa Executar SQL para inserir as séries de valores em uma linha na tabela para análise e geração de relatório posterior.  
  
     Para obter mais informações sobre essa abordagem, consulte a seção "ETL Auditing and Logging," a [!INCLUDE[msCoName](../../includes/msconame-md.md)] white paper sobre [Project REAL: Business Intelligence ETL Design Practices](https://go.microsoft.com/fwlink/?LinkId=96602).  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>Solucionar problemas de execução de pacotes por meio de arquivos de despejo de depuração  
 No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode criar arquivos de despejo de depuração que fornecem informações sobre a execução de um pacote. Para obter mais informações, consulte [Generating Dump Files for Package Execution](generating-dump-files-for-package-execution.md).  
  
## <a name="troubleshoot-run-time-validation-issues"></a>Solucionar problemas de validação em tempo de execução  
 Às vezes, você não poderá se conectar às suas fontes de dados ou validar partes de seu pacote até que as tarefas anteriores no pacote tenham sido executadas. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui os seguintes recursos para ajudar a evitar os erros de validação que resultam dessas condições:  
  
-   **Configurar uma propriedade DelayValidation em elementos de pacote que não são válidos quando o pacote estiver carregado**. `DelayValidation` pode ser definida como `True` em elementos do pacote cujas configurações não são válidas para evitar erros de validação quando o pacote for carregado. Por exemplo, você pode ter uma tarefa Fluxo de Dados que usa uma tabela de destino que não existe até que uma tarefa Executar SQL crie a tabela no tempo de execução. A propriedade `DelayValidation` pode ativada no nível do pacote ou no nível das tarefas individuais e contêineres que o pacote inclui.  
  
     A propriedade `DelayValidation` pode ser definida em uma tarefa de Fluxo de Dados, mas não em componentes de fluxo de dados individuais. Você pode conseguir um efeito semelhante definindo a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> dos componentes de fluxo de dados individuais como `false`. Entretanto, quando o valor dessa propriedade for `false`, o componente não reconhecerá as alterações para o metadados de fontes de dados externas. Ao definir como `true`, a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> poderá ajudar a evitar os problemas de bloqueio causados por bloqueios no banco de dados, especialmente quando o pacote estiver usando as transações.  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>Solucionar problemas de permissões em tempo de execução  
 Se você encontrar erros ao tentar executar os pacotes implantados usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, as contas usadas pelo Agent poderão não ter as permissões necessárias. Para obter informações sobre como solucionar problemas de pacotes executados nos trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Um pacote SSIS não é executado ao chamar o pacote SSIS a partir de uma etapa de trabalho do SQL Server Agent](https://support.microsoft.com/kb/918760). Para obter mais informações sobre como executar pacotes por meio de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Trabalhos do SQL Server Agent para pacotes](../packages/sql-server-agent-jobs-for-packages.md).  
  
 Para se conectar a fontes de dados do Excel ou do Access, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent requer uma conta com permissão para ler, gravar, criar e excluir arquivos temporários na pasta especificada pelas variáveis de ambiente TEMP e TMP.  
  
## <a name="troubleshoot-64-bit-issues"></a>Solucionar problemas de 64 bits  
  
-   **Alguns provedores de dados não estão disponíveis em plataformas de 64 bits**. Em particular, o Provedor OLE DB do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet, que é necessário para conectar as fontes de dados do Excel ou do Access, não está disponível em versões de 64 bits.  
  
## <a name="troubleshoot-errors-without-a-description"></a>Solucionar problemas de erros sem uma descrição  
 Se você encontrar um erro do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que não seja acompanhado de uma descrição, localize a descrição no [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md) e procure o erro pelo número. No momento, a lista não inclui informações para solução de problemas.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar uma saída de erro em um componente de fluxo de dados](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [Adicionando o nome da coluna de erro a uma saída de erro](https://go.microsoft.com/fwlink/?LinkId=261546)em dougbert.com.  
  
  
