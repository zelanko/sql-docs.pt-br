---
title: Criar gerenciadores de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef2ea7fa43556f0c4f12ee41101aedf396a23382
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831973"
---
# <a name="create-connection-managers"></a>Criar gerenciadores de conexões
  O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui uma variedade de gerenciadores de conexões adequados às necessidades das tarefas para se conectarem aos diferentes tipos de servidores e fontes de dados. Os gerenciadores de conexões são usados pelos componentes do fluxo de dados, que extraem e carregam dados em diferentes tipos de armazenamentos de dados, e pelos provedores de log que gravam logs em um servidor, tabela ou arquivo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Por exemplo, um pacote com uma tarefa Enviar Email usa um tipo de gerenciador de conexões para conectar-se a um servidor de protocolo SMTP (Simple Mail Transfer Protocol). Um pacote com uma tarefa Executar SQL pode usar um gerenciador de conexões OLE DB para conectar-se a um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](connection-manager/integration-services-ssis-connections.md).  
  
 Para criar automaticamente e configurar gerenciadores de conexões ao criar um novo pacote, é possível usar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O assistente também ajuda a criar e configurar origens e destinos que usam os gerenciadores de conexões. Para obter mais informações, consulte [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
 Para criar manualmente um novo gerenciador de conexões e adicioná-lo a um pacote existente, use a área **Gerenciadores de Conexões** que aparece nas guias **Fluxo de Controle**, **Fluxo de Dados**e **Manipuladores de Eventos** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] . Na área **Gerenciador de Conexões** , você escolhe o tipo de gerenciador de conexões a ser criado e então define as propriedades do gerenciador de conexões usando uma caixa de diálogo que o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] fornece. Para obter mais informações, consulte a seção “Usando a área Gerenciadores de Conexões”, mais adiante neste tópico.  
  
 Depois que o gerenciador de conexões for adicionado a um pacote, você poderá usá-lo em suas tarefas, contêineres Loop Foreach, fontes, transformações e destinos. Para obter mais informações, consulte [Tarefas do Integration Services](control-flow/integration-services-tasks.md), [Contêiner Foreach Loop](control-flow/foreach-loop-container.md) e [Fluxo de Dados](data-flow/data-flow.md).  
  
## <a name="using-the-connection-managers-area"></a>Usando a área de gerenciadores de conexões  
 Você pode criar gerenciadores de conexões enquanto a guia **Fluxo de Controle**, **Fluxo de Dados**ou **Manipuladores de Eventos** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] estiver ativa.  
  
 O diagrama a seguir mostra a área **Gerenciadores de Conexões** na guia **Fluxo de Controle** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 ![Captura de tela do designer de fluxo de controle com pacote](media/samplecontrolflow.gif "Captura de tela do designer de fluxo de controle com pacote")  
  
#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>Para adicionar, configurar ou excluir um gerenciador de conexões no Designer SSIS  
  
-   [Adicionar, excluir ou compartilhar um gerenciador de conexões em um pacote](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
-   [Definir as propriedades de um Gerenciador de Conexões](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>Provedores de 32 bits e 64 bits para gerenciadores de conexões  
 Muitos dos provedores que os gerenciadores de conexões usam estão disponíveis em versões de 32 bits e 64 bits. O ambiente de design do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é um ambiente de 32 bits e você visualiza apenas provedores de 32 bits enquanto está projetando um pacote. Portanto, você só poderá configurar um gerenciador de conexões para usar um provedor de 64 bits específico, se a versão de 32 bits do mesmo provedor também estiver instalada.  
  
 No tempo de execução, a versão correta é usada e não importa se você especificou a versão de 32 bits do provedor no tempo de design. A versão de 64 bits do provedor pode ser executada mesmo que o pacote esteja sendo executado no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Ambas as versões do provedor têm o mesmo ID. Para especificar se o tempo de execução do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa uma versão de 64 bits disponível do provedor, você define a propriedade Run64BitRuntime do projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Se a propriedade Run64BitRuntime estiver definida como `true`, o tempo de execução encontrará e usará o provedor de 64 bits; se Run64BitRuntime for `false`, o tempo de execução encontrará e usará o provedor de 32 bits. Para obter mais informações sobre as propriedades que você pode definir em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], consulte [Integration Services &#40;SSIS&#41; e Studio Environments](integration-services-ssis-development-and-management-tools.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Controle](control-flow/control-flow.md)   
 [Fluxo de Dados](data-flow/data-flow.md)   
 [Manipuladores de eventos do Integration Services &#40;SSIS&#41](integration-services-ssis-event-handlers.md)  
  
  
