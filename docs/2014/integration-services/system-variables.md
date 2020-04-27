---
title: Variáveis do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], variables
- tasks [Integration Services], variables
- system variables [Integration Services]
- event handlers [Integration Services], variables
- variables [Integration Services], system
ms.assetid: efecd0d4-1489-4eba-a8fe-275d647058b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 58254a5c9f9031e4657f7a3a2eb5cb73be4fbdea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62927215"
---
# <a name="system-variables"></a>Variáveis do sistema
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece um conjunto de variáveis de sistema que armazena informações sobre o pacote em execução e seus objetos. Essas variáveis podem ser usadas em expressões e expressões de propriedade para personalizar pacotes, contêineres, tarefas e manipuladores de eventos.  
  
 Todas as variáveis do sistema e as definidas pelo usuário podem ser usadas nas associações de parâmetro que a tarefa Executar SQL usa para mapear variáveis para parâmetros.  
  
## <a name="system-variables-for-packages"></a>Variáveis do sistema para pacotes  
 A tabela a seguir descreve as variáveis do sistema que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece para pacotes.  
  
|Variável do sistema|Tipo de dados|DESCRIÇÃO|  
|---------------------|---------------|-----------------|  
|**CancelEvent**|Int32|O manipulador de um objeto de Evento do Windows que a tarefa pode sinalizar para indicar que a execução da tarefa deve ser interrompida.|  
|`ContainerStartTime`|Datetime|A hora de início do contêiner.|  
|**CreationDate**|Datetime|A data em que o pacote foi criado.|  
|`CreatorComputerName`|String|O computador no qual o pacote foi criado.|  
|**CreatorName**|String|O nome da pessoa que criou o pacote.|  
|`ExecutionInstanceGUID`|String|O identificador exclusivo da instância de execução de um pacote.|  
|`FailedConfigurations`|String|Os nomes das configurações de pacote que falharam.|  
|`IgnoreConfigurationsOnLoad`|Boolean|Indica se as configurações de pacote são ignoradas ao carregar o pacote.|  
|**InteractiveMode**|Boolean|Indica se o pacote é executado em modo interativo. Se um pacote estiver sendo executado no [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, essa propriedade será definida como `True`. Se um pacote estiver em execução usando o utilitário de prompt de comando **dtexec** , a propriedade `False`será definida como.|  
|`LocaleId`|Int32|A localidade que o pacote usa.|  
|**MachineName**|String|O nome do computador no qual o pacote está sendo executado.|  
|**OfflineMode**|Boolean|Indica se o pacote está no modo offline. O modo offline não obtém conexões com fontes de dados.|  
|**PackageID**|String|O identificador exclusivo do pacote.|  
|**PackageName**|String|O nome do pacote.|  
|**StartTime**|Datetime|A hora de início da execução do pacote.|  
|`ServerExecutionID`|Int64|A ID da execução para o pacote executado no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .<br /><br /> O valor padrão é zero. O valor só será alterado se o pacote for executado pelo ISServerExec no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Server. Quando houver um pacote filho, o valor será transmitido do pacote pai para o pacote filho.|  
|**Usu**|String|A conta do usuário que iniciou o pacote. O nome do usuário é qualificado pelo nome do domínio.|  
|**VersionBuild**|Int32|A versão do pacote.|  
|**VersionComment**|String|Comentários sobre a versão do pacote.|  
|**VersionGUID**|String|O identificador exclusivo da versão.|  
|**VersionMajor**|Int32|A versão principal do pacote.|  
|**VersionMinor**|Int32|A versão secundária do pacote.|  
  
## <a name="system-variables-for-containers"></a>Variáveis do sistema para contêineres  
 A tabela a seguir descreve as variáveis do sistema que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece para os contêineres Loop For, Loop Foreach e Sequência.  
  
|Variável do sistema|Tipo de dados|Descrição|Contêiner|  
|---------------------|---------------|-----------------|---------------|  
|`LocaleId`|Int32|A localidade que o contêiner usa.|Contêiner Loop For<br /><br /> Contêiner Loop Foreach<br /><br /> Contêiner de sequência|  
  
## <a name="system-variables-for-tasks"></a>Variáveis do sistema para tarefas  
 A tabela a seguir descreve as variáveis do sistema que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece para tarefas.  
  
|Variável do sistema|Tipo de dados|Descrição|  
|---------------------|---------------|-----------------|  
|**CreationName**|String|O nome da tarefa.|  
|`LocaleId`|Int32|A localidade que a tarefa usa.|  
|**TaskID**|String|O identificador exclusivo da instância de uma tarefa.|  
|**TaskName**|String|O nome da instância da tarefa.|  
|`TaskTransactionOption`|Int32|A opção de transação que a tarefa usa.|  
  
## <a name="system-variables-for-event-handlers"></a>Variáveis do sistema para Manipuladores de Eventos  
 A tabela seguinte descreve as variáveis do sistema que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece para manipuladores de eventos. Nem todas as variáveis estão disponíveis para todos os manipuladores de eventos.  
  
|Variável do sistema|Tipo de dados|Descrição|Manipulador de eventos|  
|---------------------|---------------|-----------------|-------------------|  
|**Cancelar**|Boolean|Indica se a execução do manipulador de eventos é interrompida quando ocorre um erro, aviso ou cancelamento de consulta.|Manipulador de eventos OnError<br /><br /> Manipulador de eventos OnWarning<br /><br /> Manipulador de eventos OnQueryCancel|  
|**ErrorCode**|Int32|O identificador do erro.|Manipulador de eventos OnError<br /><br /> Manipulador de eventos OnInformation<br /><br /> Manipulador de eventos OnWarning|  
|**ErrorDescription**|String|A descrição do erro.|Manipulador de eventos OnError<br /><br /> Manipulador de eventos OnInformation<br /><br /> Manipulador de eventos OnWarning|  
|**ExecutionStatus**|Boolean|O status de execução atual.|Manipulador de eventos OnExecStatusChanged|  
|`ExecutionValue`|DBNull|O valor da execução.|Manipulador de eventos OnTaskFailed|  
|`LocaleId`|Int32|A localidade que o manipulador de eventos usa.|Todos os manipuladores de eventos|  
|**PercentComplete**|Int32|A porcentagem do trabalho concluído.|Manipulador de eventos OnProgress|  
|**ProgressCountHigh**|Int32|A parte alta de um valor de 64 bits que indica o número total de operações processadas pelo evento OnProgress.|Manipulador de eventos OnProgress|  
|`ProgressCountLow`|Int32|A parte baixa de um valor de 64 bits que indica o número total de operações processadas pelo evento OnProgress.|Manipulador de eventos OnProgress|  
|**ProgressDescription**|String|Descrição do progresso.|Manipulador de eventos OnProgress|  
|`Propagate`|Boolean|Indica se o evento é propagado para um manipulador de eventos de nível mais alto.<br /><br /> Observação: o valor da variável `Propagate` é desconsiderado durante a validação do pacote.<br /><br /> Se você definir `Propagate` como `False` em um pacote filho, isto não impedirá que um evento seja propagado até o pacote pai.|Todos os manipuladores de eventos|  
|`SourceDescription`|String|A descrição do executável no manipulador de eventos que ativou o evento.|Todos os manipuladores de eventos|  
|`SourceID`|String|O identificador exclusivo do executável no manipulador de eventos que ativou o evento.|Todos os manipuladores de eventos|  
|**SourceName**|String|O nome do executável no manipulador de eventos que ativou o evento.|Todos os manipuladores de eventos|  
|`VariableDescription`|String|A descrição da variável.|Manipulador de eventos OnVariableValueChanged|  
|`VariableID`|String|O identificador exclusivo da variável.|Manipulador de eventos OnVariableValueChanged|  
  
## <a name="system-variables-in-parameter-bindings"></a>Variáveis do sistema em associações de parâmetros  
 É muito útil salvar os valores de variáveis do sistema em tabelas quando o pacote é executado. Por exemplo, um pacote que cria dinamicamente uma tabela e grava o GUID da instância de execução do pacote que criou a tabela em uma coluna da tabela.  
  
 Se você usar variáveis do sistema para mapear parâmetros na instrução SQL que uma tarefa Executar SQL usa, é importante definir o tipo de dados de cada parâmetro associado ao tipo de dados da variável do sistema. Caso contrário, os valores de variáveis do sistema poderão ser convertidos incorretamente. Por exemplo, se a variável do sistema `ExecutionInstanceGUID`, que contém o tipo de dados de cadeia de caracteres, e a cadeia que representa o GUID da instância em execução de um pacote for usada em um parâmetro associado ao tipo de dados GUID, o GUID da instância do pacote será convertido incorretamente.  
  
 Essa regra se aplica também a variáveis definidas pelo usuário. Mas, enquanto os tipos de dados de variáveis do sistema não podem ser alterados e você precisa moldar o uso dessas variáveis para se ajustar aos tipos de dados, aqueles definidos pelo usuário são mais flexíveis. As variáveis definidas pelo usuário e usadas em associações de parâmetro são geralmente definidas com tipos de dados compatíveis aos tipos de dados dos parâmetros para os quais são mapeados.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Mapear parâmetros de consulta para variáveis em uma tarefa Executar SQL](control-flow/execute-sql-task.md)  
  
  
