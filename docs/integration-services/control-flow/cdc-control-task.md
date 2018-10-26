---
title: Tarefa Controle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdccontroltask.f1
- sql13.ssis.designer.cdccontroltask.config.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74609a50ad4d2f29bbbd7d25cc4cd1a242e64ff4
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49071750"
---
# <a name="cdc-control-task"></a>Tarefa Controle de CDC
  A tarefa Controle de CDC é usada para controlar o ciclo de vida de pacotes de captura de dados de alterações (CDC). Ela trata a sincronização de pacotes CDC com o pacote de carga inicial e o gerenciamento de intervalos de LSN (número de sequência de log) processados na execução de um pacote CDC. Além disso, a tarefa Controle de CDC lida com cenários de erro e recuperação.  
  
 A tarefa Controle de CDC mantém o estado do pacote CDC em uma variável de pacote SSIS e também pode persisti-lo em uma tabela de banco de dados para que o estado seja mantido nas ativações de pacote e entre vários pacotes que juntos executam um processo CDC comum (por exemplo, uma tarefa pode ser responsável pelo carregamento inicial e a outra pelas atualizações trickle-feed).  
  
 A tarefa Controle de CDC oferece suporte a dois grupos de operações. Um grupo trata a sincronização de carga inicial e processamento de alteração e o outro gerencia o intervalo do processamento de alteração de LSNs para uma execução de um pacote CDC e acompanha o que foi processada com êxito.  
  
 As operações seguintes tratam a sincronização da carga inicial e o processamento de alteração:  
  
|Operação|Descrição|  
|---------------|-----------------|  
|ResetCdcState|Esta operação é usada para reiniciar o estado de CDC persistente associado ao contexto de CDC atual. Depois que esta operação é executada, o LSN máximo atual da tabela `sys.fn_cdc_get_max_lsn` do carimbo de data/hora de LSN torna-se o início do intervalo para o próximo intervalo de processamento. Esta operação exige uma conexão com o banco de dados de origem.|  
|MarkInitialLoadStart|Esta operação é usada no começo de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem antes de o pacote da carga inicial começar a ler as tabelas de origem. Isso exige uma conexão com o banco de dados de origem para chamar `sys.fn_cdc_get_max_lsn`.<br /><br /> Se você selecionar MarkInitialLoadStart ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser db_owner ou sysadmin.|  
|MarkInitialLoadEnd|A operação é usada no início de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem depois de o pacote da carga inicial terminar de ler as tabelas de origem. Este LSN é determinado pela gravação da hora atual quando esta operação ocorreu e, em seguida, consultando a tabela de mapeamento `cdc.lsn_time_`no banco de dados CDC, procurando uma alteração que ocorreu depois daquele momento<br /><br /> Se você selecionar MarkInitialLoadEnd ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser db_owner ou sysadmin.|  
|MarkCdcStart|Esta operação é usada quando a carga inicial é feita de um banco de dados de instantâneo. Nesse caso, o processamento de alteração deve ser iniciado imediatamente depois do LSN do instantâneo. Você pode especificar o nome do banco de dados de instantâneo a ser usado e a tarefa Controle de CDC consulta o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para obter o LSN de instantâneo. Você também tem a opção de especificar diretamente o LSN de instantâneo.<br /><br /> Se você selecionar MarkCdcStart ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser db_owner ou sysadmin.|  
  
 As operações seguintes são usadas para gerenciar o intervalo de processamento:  
  
|Operação|Descrição|  
|---------------|-----------------|  
|GetProcessingRange|Esta operação é usada antes da chamada ao fluxo de dados que usa o fluxo de dados de Origem CDC. Ele estabelece um intervalo de LSNs que o fluxo de dados de origem de CDC lê quando é invocado. O intervalo é armazenado em uma variável de pacote SSIS que é usada pela Origem de CDC durante o processamento de fluxo de dados.<br /><br /> Para obter mais informações sobre os armazenados, consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).|  
|MarkProcessedRange|: Esta operação é executada depois de cada execução de CDC (depois que o fluxo de dados de CDC é concluído com êxito) para registrar o último LSN que foi processado completamente na execução de CDC. Da próxima vez que o GetProcessingRange for executado, essa posição será o início do intervalo de processamento.|  
  
## <a name="handling-cdc-state-persistency"></a>Lidando com a persistência de estado CDC  
 A tarefa Controle de CDC mantém um estado persistente entre ativações. As informações armazenadas no estado CDC são usadas para determinar e manter o intervalo de processamento do pacote CDC e para detectar condições de erro. O estado persistente é armazenado como uma cadeia de caracteres. Para obter mais informações, consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).  
  
 A tarefa Controle de CDC oferece suporte a dois tipos de persistência de estado  
  
-   Persistência de Estado Manual: nesse caso, a tarefa Controle de CDC gerencia o estado armazenado em uma variável de pacote, mas o desenvolvedor do pacote deve ler a variável de um repositório persistente antes de chamar o Controle de CDC e depois gravá-lo nesse repositório persistente após o Controle de CDC ser chamado pela última vez e a execução do CDC for concluída.  
  
-   Persistência de Estado Automática: o estado CDC é armazenado em uma tabela em um banco de dados. O estado é armazenado com um nome fornecido na propriedade **StateName** em uma tabela nomeada na propriedade **Tabela a Ser Usada para Armazenar o Estado** , localizada em um gerenciador de conexões selecionado para armazenar o estado. O padrão é o gerenciador de conexões de origem, mas a prática comum é usar o gerenciador de conexões de destino. A tarefa Controle de CDC atualiza o valor do estado na tabela de estado e isso é confirmado como parte da transação de ambiente.  
  
## <a name="error-handling"></a>Tratamento de erros  
 A tarefa Controle de CDC pode relatar um erro quando:  
  
-   Não lê o estado persistente do CDC ou ao quando a atualização do estado persistente falha.  
  
-   Não lê as informações de LSN atuais do banco de dados de origem.  
  
-   O estado CDC lido não é consistente.  
  
 Em todos esses casos, a tarefa Controle de CDC relata um erro que pode ser tratado do modo padrão como o SSIS trata erros de fluxo de controle.  
  
 A tarefa Controle de CDC também pode relatar um aviso quando a operação Obter Intervalo de Processamento é chamada diretamente depois de outra operação do mesmo tipo sem que Marcar Intervalo Processado seja chamada. Essa é uma indicação de que a execução anterior falhou ou que outro pacote CDC pode estar sendo executado com o mesmo nome do estado CDC.  
  
## <a name="configuring-the-cdc-control-task"></a>Configurando a tarefa Controle de CDC  
 Você pode definir as propriedades por meio do Designer SSIS ou programaticamente.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades personalizadas da tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico [Instalando o Change Data Capture do Microsoft SQL Server 2012 para Oracle da Attunity](http://go.microsoft.com/fwlink/?LinkId=252958)em social.technet.microsoft.com.  
  
-   Artigo técnico [Solucionando problemas de configuração do Microsoft Change Data Capture para Oracle da Attunity](http://go.microsoft.com/fwlink/?LinkId=252960)em social.technet.microsoft.com.  
  
-   Artigo técnico [Solucionando erros de instância CDC no Microsoft Change Data Capture para Oracle da Attunity](http://go.microsoft.com/fwlink/?LinkId=252961)em social.technet.microsoft.com.  
  
## <a name="cdc-control-task-editor"></a>CDC Control Task Editor
  Use a caixa de diálogo **Editor da tarefa Controle CDC** para configurar a tarefa Controle CDC. A configuração da tarefa Controle CDC inclui definir uma conexão para o banco de dados CDC, a operação de tarefa CDC e as informações de gerenciamento de estado.  
  
 Para obter mais informações sobre a tarefa Controle CDC, consulte [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 **Para abrir o Editor da tarefa Controle CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que contém a tarefa Controle CDC.  
  
2.  Na guia **Fluxo de Controle** , clique duas vezes na tarefa Controle CDC.  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões ADO.NET do banco de dados SQL Server CDC**  
 Selecione na lista um gerenciador de conexões existente ou clique em **Novo** para criar uma nova conexão. A conexão deve ser a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitado para CDC e onde a tabela de alteração selecionada está localizada.  
  
 **Operação de Controle CDC**  
 Selecione a operação a ser executada para esta tarefa. Todas as operações usam a variável de estado que está armazenada em uma variável de pacote SSIS que armazena o estado e passa isto entre os diferentes componentes no pacote.  
  
-   **Marcar início da carga inicial**: esta operação é usada ao executar uma carga inicial de um banco de dados ativo sem um instantâneo. Ela é invocada no começo de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem antes de o pacote da carga inicial começar a ler as tabelas de origem. Isto exige uma conexão com o banco de dados de origem.  
  
     Se você selecionar **Marcar início da carga inicial** ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser  **db_owner** ou **sysadmin**.  
  
-   **Marcar fim da carga inicial**: esta operação é usada ao executar uma carga inicial de um banco de dados ativo sem um instantâneo. Ela é invocada no início de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem depois de o pacote da carga inicial terminar de ler as tabelas de origem. Este LSN é determinado pela gravação da hora atual quando esta operação ocorreu e, em seguida, consultando a tabela de mapeamento `cdc.lsn_time_`no banco de dados CDC, procurando uma alteração que ocorreu depois daquele momento  
  
     Se você selecionar **Marcar fim da carga inicial** ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser  **db_owner** ou **sysadmin**.  
  
-   **Marcar início do CDC**: esta operação é usada quando a carga inicial é feita de um banco de dados de instantâneo ou de um banco de dados fechado para novas sessões. Ele é invocado em qualquer ponto dentro do pacote de carga inicial. A operação aceita um parâmetro que pode ser um LSN instantâneo, um nome de um banco de dados de instantâneo (do qual o LSN instantâneo será derivado automaticamente) ou pode ser deixado vazio e, nesse caso, o LSN do banco de dados atual será usado como o LSN inicial para o pacote de processamento de alteração.  
  
     Esta operação é usada em vez das operações Marcar início/fim da carga inicial.  
  
     Se você selecionar **Marcar início de CDC** ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser  **db_owner** ou **sysadmin**.  
  
-   **Obter intervalo de processamento**: esta operação é usada em um pacote de processamento de alteração antes de invocar o fluxo de dados que usa o fluxo de dados de Origem de CDC. Ele estabelece um intervalo de LSNs que o fluxo de dados de origem de CDC lê quando é invocado. O intervalo é armazenado em uma variável de pacote SSIS que é usada pela Origem de CDC durante o processamento de fluxo de dados.  
  
     Para obter mais informações sobre os possíveis estados de CDC que estão armazenados, consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).  
  
-   **Marcar o intervalo processado**: esta operação é usada em um pacote de processamento de alteração no fim de uma execução de CDC (depois que o fluxo de dados de CDC é concluído com êxito) para registrar o último LSN que foi processado completamente na execução de CDC. Da próxima vez que o `GetProcessingRange` é executado, esta posição determina o início do próximo intervalo de processamento.  
  
-   **Reiniciar estado de CDC**: esta operação é usada para reiniciar o estado de CDC persistente associado ao contexto de CDC atual. Depois que esta operação é executada, o LSN máximo atual da tabela `sys.fn_cdc_get_max_lsn` do carimbo de data/hora de LSN torna-se o início do intervalo para o próximo intervalo de processamento. Esta operação exige uma conexão com o banco de dados de origem.  
  
     Um exemplo de quando esta operação é usada é quando você deseja processar somente os registros de alteração recém-criados e ignorar todos os registros de alteração antigos.  
  
 **Variável contendo o estado de CDC**  
 Selecione a variável de pacote SSIS que armazena as informações do estado para a operação de tarefa. Você deve definir uma variável antes de começar. Se você selecionar **Persistência de estado automática**, a variável de estado será carregada e salva automaticamente.  
  
 Para obter mais informações sobre como definir a variável de estado, consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).  
  
 **LSN do SQL Server para começar o nome do CDC/instantâneo:**  
 Digite o LSN de banco de dados de origem atual ou o nome do banco de dados de instantâneo do qual a carga inicial é realizada para determinar onde o CDC inicia. Isto só está disponível se o **Operação de Controle CDC** é definido como **Marcar início do CDC**.  
  
 Para obter mais informações sobre essas operações, consulte [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 **Armazene o estado automaticamente em uma tabela de banco de dados**  
 Marque esta caixa de seleção para a tarefa de Controle CDC para tratar o carregamento automaticamente e armazenar o estado de CDC em uma tabela de estado contida no banco de dados especificado. Quando não estiver selecionado, o desenvolvedor deverá carregar o Estado de CDC quando o pacote iniciar e salvá-lo sempre que o Estado de CDC for alterado.  
  
 **Gerenciador de conexões para o banco de dados onde o estado está armazenado**  
 Selecione na lista um gerenciador de conexões ADO.NET existente ou clique em Novo para criar uma nova conexão. Esta conexão é para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a tabela de estado. A tabela de Estado contém as informações do estado.  
  
 Isto só estará disponível se **Persistência de estado automática** estiver selecionada e for um parâmetro necessário.  
  
 **Tabela para usar para armazenar estado**  
 Digite o nome da tabela de estado a ser usada para armazenar o estado CDC. A tabela especificada deve ter duas colunas chamadas **nome** e **estado** e ambas as colunas devem ser do tipo de dados **varchar (256)**.  
  
 Você pode opcionalmente selecionar **Novo** para obter um script SQL que cria uma nova tabela de estado com as colunas necessárias. Quando **Persistência de estado automática** estiver selecionada, o desenvolvedor deverá criar uma tabela de estado de acordo com os requisitos listados acima.  
  
 Isto só estará disponível se **Persistência de estado automática** estiver selecionada e for um parâmetro necessário.  
  
 **Nome do estado**  
 Digite um nome para associar com o estado de CDC persistente. A carga cheia e os pacotes CDC que funcionam com o mesmo contexto de CDC especificará um nome de estado comum. Esse nome é usado para verificar a linha de estado na tabela de estado  
  
