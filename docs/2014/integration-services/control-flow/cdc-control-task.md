---
title: Tarefa Controle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1ddc919b4658395c6a4268f03131bc92291f1b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62832878"
---
# <a name="cdc-control-task"></a>Tarefa Controle de CDC
  A tarefa Controle de CDC é usada para controlar o ciclo de vida de pacotes de captura de dados de alterações (CDC). Ela trata a sincronização de pacotes CDC com o pacote de carga inicial e o gerenciamento de intervalos de LSN (número de sequência de log) processados na execução de um pacote CDC. Além disso, a tarefa Controle de CDC lida com cenários de erro e recuperação.  
  
 A tarefa Controle de CDC mantém o estado do pacote CDC em uma variável de pacote SSIS e também pode persisti-lo em uma tabela de banco de dados para que o estado seja mantido nas ativações de pacote e entre vários pacotes que juntos executam um processo CDC comum (por exemplo, uma tarefa pode ser responsável pelo carregamento inicial e a outra pelas atualizações trickle-feed).  
  
 A tarefa Controle de CDC oferece suporte a dois grupos de operações. Um grupo trata a sincronização de carga inicial e processamento de alteração e o outro gerencia o intervalo do processamento de alteração de LSNs para uma execução de um pacote CDC e acompanha o que foi processada com êxito.  
  
 As operações seguintes tratam a sincronização da carga inicial e o processamento de alteração:  
  
|Operação|DESCRIÇÃO|  
|---------------|-----------------|  
|ResetCdcState|Esta operação é usada para reiniciar o estado de CDC persistente associado ao contexto de CDC atual. Depois que esta operação é executada, o LSN máximo atual da tabela `sys.fn_cdc_get_max_lsn` do carimbo de data/hora de LSN torna-se o início do intervalo para o próximo intervalo de processamento. Esta operação exige uma conexão com o banco de dados de origem.|  
|MarkInitialLoadStart|Esta operação é usada no começo de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem antes de o pacote da carga inicial começar a ler as tabelas de origem. Isso exige uma conexão com o banco de dados de origem para chamar `sys.fn_cdc_get_max_lsn`.<br /><br /> Se você selecionar MarkInitialLoadStart ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser db_owner ou sysadmin.|  
|MarkInitialLoadEnd|A operação é usada no início de um pacote da carga inicial para registrar o LSN atual no banco de dados de origem depois de o pacote da carga inicial terminar de ler as tabelas de origem. Este LSN é determinado pela gravação da hora atual quando esta operação ocorreu e, em seguida, consultando a tabela de mapeamento `cdc.lsn_time_`no banco de dados CDC, procurando uma alteração que ocorreu depois daquele momento<br /><br /> Se você selecionar MarkInitialLoadEnd ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser db_owner ou sysadmin.|  
|MarkCdcStart|Esta operação é usada quando a carga inicial é feita de um banco de dados de instantâneo. Nesse caso, o processamento de alteração deve ser iniciado imediatamente depois do LSN do instantâneo. Você pode especificar o nome do banco de dados de instantâneo a ser usado e a tarefa Controle de CDC consulta o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para obter o LSN de instantâneo. Você também tem a opção de especificar diretamente o LSN de instantâneo.<br /><br /> Se você selecionar MarkCdcStart ao trabalhar no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (ou seja, não Oracle), o usuário especificado no gerenciador de conexões deverá ser db_owner ou sysadmin.|  
  
 As operações seguintes são usadas para gerenciar o intervalo de processamento:  
  
|Operação|DESCRIÇÃO|  
|---------------|-----------------|  
|GetProcessingRange|Esta operação é usada antes da chamada ao fluxo de dados que usa o fluxo de dados de Origem CDC. Ele estabelece um intervalo de LSNs que o fluxo de dados de origem de CDC lê quando é invocado. O intervalo é armazenado em uma variável de pacote SSIS que é usada pela Origem de CDC durante o processamento de fluxo de dados.<br /><br /> Para obter mais informações sobre os armazenados, consulte [Definir uma variável de estado](../data-flow/define-a-state-variable.md).|  
|MarkProcessedRange|: Esta operação é executada depois de cada execução de CDC (depois que o fluxo de dados de CDC é concluído com êxito) para registrar o último LSN que foi processado completamente na execução de CDC. Da próxima vez que o GetProcessingRange for executado, essa posição será o início do intervalo de processamento.|  
  
## <a name="handling-cdc-state-persistency"></a>Lidando com a persistência de estado CDC  
 A tarefa Controle de CDC mantém um estado persistente entre ativações. As informações armazenadas no estado CDC são usadas para determinar e manter o intervalo de processamento do pacote CDC e para detectar condições de erro. O estado persistente é armazenado como uma cadeia de caracteres. Para obter mais informações, consulte [Definir uma variável de estado](../data-flow/define-a-state-variable.md).  
  
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
  
-   [Editor da Tarefa Controle de CDC](../cdc-control-task-editor.md)  
  
-   [Propriedades personalizadas da tarefa Controle de CDC](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir uma variável de estado](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Artigo técnico [Instalando o Change Data Capture do Microsoft SQL Server 2012 para Oracle da Attunity](https://go.microsoft.com/fwlink/?LinkId=252958)em social.technet.microsoft.com.  
  
-   Artigo técnico [Solucionando problemas de configuração do Microsoft Change Data Capture para Oracle da Attunity](https://go.microsoft.com/fwlink/?LinkId=252960)em social.technet.microsoft.com.  
  
-   Artigo técnico [Solucionando erros de instância CDC no Microsoft Change Data Capture para Oracle da Attunity](https://go.microsoft.com/fwlink/?LinkId=252961)em social.technet.microsoft.com.  
  
  
