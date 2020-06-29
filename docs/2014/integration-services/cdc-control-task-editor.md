---
title: Editor da tarefa controle de CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.config.f1
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 35d20d475b8f6da9c899c389419233f8e90bf555
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439013"
---
# <a name="cdc-control-task-editor"></a>CDC Control Task Editor
  Use a caixa de diálogo **Editor da tarefa Controle CDC** para configurar a tarefa Controle CDC. A configuração da tarefa Controle CDC inclui definir uma conexão para o banco de dados CDC, a operação de tarefa CDC e as informações de gerenciamento de estado.  
  
 Para obter mais informações sobre a tarefa Controle CDC, consulte [CDC Control Task](control-flow/cdc-control-task.md).  
  
 **Para abrir o Editor da tarefa Controle CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote do [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que contém a tarefa Controle CDC.  
  
2.  Na guia **Fluxo de Controle** , clique duas vezes na tarefa Controle CDC.  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões ADO.NET do banco de dados SQL Server CDC**  
 Selecione na lista um gerenciador de conexões existente ou clique em **Novo** para criar uma nova conexão. A conexão deve ser a um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que está habilitado para CDC e onde a tabela de alteração selecionada está localizada.  
  
 **Operação de Controle CDC**  
 Selecione a operação a ser executada para esta tarefa. Todas as operações usam a variável de estado que está armazenada em uma variável de pacote SSIS que armazena o estado e passa isto entre os diferentes componentes no pacote.  
  
-   **Marcar início da carga inicial**: esta operação é usada ao executar uma carga inicial de um banco de dados ativo sem um instantâneo. Ela é invocada no começo de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem antes de o pacote da carga inicial começar a ler as tabelas de origem. Isto exige uma conexão com o banco de dados de origem.  
  
     Se você selecionar **Marcar início da carga inicial** ao trabalhar no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser  **db_owner** ou **sysadmin**.  
  
-   **Marcar fim da carga inicial**: esta operação é usada ao executar uma carga inicial de um banco de dados ativo sem um instantâneo. Ela é invocada no início de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem depois de o pacote da carga inicial terminar de ler as tabelas de origem. Este LSN é determinado pela gravação da hora atual quando esta operação ocorreu e, em seguida, consultando a tabela de mapeamento `cdc.lsn_time_`no banco de dados CDC, procurando uma alteração que ocorreu depois daquele momento  
  
     Se você selecionar **Marcar fim da carga inicial** ao trabalhar no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser  **db_owner** ou **sysadmin**.  
  
-   **Marcar início do CDC**: esta operação é usada quando a carga inicial é feita de um banco de dados de instantâneo ou de um banco de dados fechado para novas sessões. Ele é invocado em qualquer ponto dentro do pacote de carga inicial. A operação aceita um parâmetro que pode ser um LSN instantâneo, um nome de um banco de dados de instantâneo (do qual o LSN instantâneo será derivado automaticamente) ou pode ser deixado vazio e, nesse caso, o LSN do banco de dados atual será usado como o LSN inicial para o pacote de processamento de alteração.  
  
     Esta operação é usada em vez das operações Marcar início/fim da carga inicial.  
  
     Se você selecionar **Marcar início de CDC** ao trabalhar no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser  **db_owner** ou **sysadmin**.  
  
-   **Obter intervalo de processamento**: esta operação é usada em um pacote de processamento de alteração antes de invocar o fluxo de dados que usa o fluxo de dados de Origem de CDC. Ele estabelece um intervalo de LSNs que o fluxo de dados de origem de CDC lê quando é invocado. O intervalo é armazenado em uma variável de pacote SSIS que é usada pela Origem de CDC durante o processamento de fluxo de dados.  
  
     Para obter mais informações sobre os possíveis estados de CDC que estão armazenados, consulte [Definir uma variável de estado](data-flow/define-a-state-variable.md).  
  
-   **Marcar o intervalo processado**: esta operação é usada em um pacote de processamento de alteração no fim de uma execução de CDC (depois que o fluxo de dados de CDC é concluído com êxito) para registrar o último LSN que foi processado completamente na execução de CDC. Da próxima vez que o `GetProcessingRange` é executado, esta posição determina o início do próximo intervalo de processamento.  
  
-   **Reiniciar estado de CDC**: esta operação é usada para reiniciar o estado de CDC persistente associado ao contexto de CDC atual. Depois que esta operação é executada, o LSN máximo atual da tabela `sys.fn_cdc_get_max_lsn` do carimbo de data/hora de LSN torna-se o início do intervalo para o próximo intervalo de processamento. Esta operação exige uma conexão com o banco de dados de origem.  
  
     Um exemplo de quando esta operação é usada é quando você deseja processar somente os registros de alteração recém-criados e ignorar todos os registros de alteração antigos.  
  
 **Variável contendo o estado de CDC**  
 Selecione a variável de pacote SSIS que armazena as informações do estado para a operação de tarefa. Você deve definir uma variável antes de começar. Se você selecionar **Persistência de estado automática**, a variável de estado será carregada e salva automaticamente.  
  
 Para obter mais informações sobre como definir a variável de estado, consulte [Definir uma variável de estado](data-flow/define-a-state-variable.md).  
  
 **LSN do SQL Server para começar o nome do CDC/instantâneo:**  
 Digite o LSN de banco de dados de origem atual ou o nome do banco de dados de instantâneo do qual a carga inicial é realizada para determinar onde o CDC inicia. Isto só está disponível se o **Operação de Controle CDC** é definido como **Marcar início do CDC**.  
  
 Para obter mais informações sobre essas operações, consulte [CDC Control Task](control-flow/cdc-control-task.md).  
  
 **Armazene o estado automaticamente em uma tabela de banco de dados**  
 Marque esta caixa de seleção para a tarefa de Controle CDC para tratar o carregamento automaticamente e armazenar o estado de CDC em uma tabela de estado contida no banco de dados especificado. Quando não estiver selecionado, o desenvolvedor deverá carregar o Estado de CDC quando o pacote iniciar e salvá-lo sempre que o Estado de CDC for alterado.  
  
 **Gerenciador de conexões para o banco de dados onde o estado está armazenado**  
 Selecione na lista um gerenciador de conexões ADO.NET existente ou clique em Novo para criar uma nova conexão. Esta conexão é para um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contém a tabela de estado. A tabela de Estado contém as informações do estado.  
  
 Isto só estará disponível se **Persistência de estado automática** estiver selecionada e for um parâmetro necessário.  
  
 **Tabela para usar para armazenar estado**  
 Digite o nome da tabela de estado a ser usada para armazenar o estado CDC. A tabela especificada deve ter duas colunas chamadas **nome** e **estado** e ambas as colunas devem ser do tipo de dados **varchar (256)**.  
  
 Você pode opcionalmente selecionar **Novo** para obter um script SQL que cria uma nova tabela de estado com as colunas necessárias. Quando **Persistência de estado automática** estiver selecionada, o desenvolvedor deverá criar uma tabela de estado de acordo com os requisitos listados acima.  
  
 Isto só estará disponível se **Persistência de estado automática** estiver selecionada e for um parâmetro necessário.  
  
 **Nome do estado**  
 Digite um nome para associar com o estado de CDC persistente. A carga cheia e os pacotes CDC que funcionam com o mesmo contexto de CDC especificará um nome de estado comum. Esse nome é usado para verificar a linha de estado na tabela de estado  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades personalizadas da tarefa Controle de CDC](control-flow/cdc-control-task-custom-properties.md)  
  
  
