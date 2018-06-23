---
title: Adicionar um manipulador de eventos a um pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 68d5ed9e638c03b1a34f221ff7e61d8a0df1a454
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009185"
---
# <a name="add-an-event-handler-to-a-package"></a>Adicionar um manipulador de eventos a um pacote
  No momento da execução, contêineres e tarefas elevam os eventos. Você pode criar manipuladores de eventos personalizados que respondam a esses eventos, executando um fluxo de trabalho quando o evento for gerado. Por exemplo, você pode criar um manipulador de eventos que envia uma mensagem de e-mail quando uma tarefa falha.  
  
 Um manipulador de eventos é semelhante a um pacote. Como um pacote, um manipulador de eventos pode fornecer escopo para variáveis e incluir um fluxo de controle e fluxos de dados opcionais. Você pode criar manipuladores de eventos para pacotes, o contêiner Loop Foreach, o contêiner Loop For, o contêiner Sequência e todas as tarefas.  
  
 Você cria manipuladores de eventos usando a superfície de design da guia **Manipuladores de Eventos** no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 Quando a guia **Manipuladores de Eventos** está ativa, os nós **Itens de Fluxo de Controle** e **Tarefas de Plano de Manutenção** da Caixa de Ferramentas no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] contêm a tarefa e contêineres para criar o fluxo de controle do manipulador de eventos. Os nós **Origens de Fluxo de Dados**, **Transformações**e **Destinos de Fluxos de Dados** contêm as fontes de dados, transformações e destinos para criar os fluxos de dados no manipulador de eventos. Para obter mais informações, consulte [Fluxo de Controle](control-flow/control-flow.md) e [Fluxo de Dados](data-flow/data-flow.md).  
  
 A guia **Manipuladores de Eventos** também inclui a área Gerenciadores de **Conexões** , em que você pode criar e modificar os gerenciadores de conexões que os manipuladores de eventos usam para conectar servidores e fontes de dados. Para obter mais informações, consulte [Criar gerenciadores de conexões](../../2014/integration-services/create-connection-managers.md).  
  
### <a name="to-create-an-event-handler"></a>Para criar um manipulador de eventos  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Manipuladores de Eventos** .  
  
     ![Captura de tela da área de design com o manipulador de eventos](media/eventhandlers.gif "Captura de tela da área de design com o manipulador de eventos")  
  
     Criar o fluxo de controle e os fluxos de dados em um manipulador de eventos é semelhante a criar o fluxo de controle e os fluxos de dados em um pacote. Para obter mais informações, consulte [Fluxo de Controle](control-flow/control-flow.md) e [Fluxo de Dados](data-flow/data-flow.md).  
  
4.  Na lista **Executável** , selecione o executável para o qual você quer criar um manipulador de eventos.  
  
5.  Na lista **Manipulador de Eventos** , selecione o manipulador de eventos que você quer criar.  
  
6.  Clique no link na superfície de design da guia **Manipulador de Eventos** .  
  
7.  Adicione itens de fluxo de controle ao manipulador de eventos e conecte itens usando uma restrição de precedência arrastando a restrição de um item de controle de fluxo para outro. Para obter mais informações, consulte [Control Flow](control-flow/control-flow.md).  
  
8.  Opcionalmente, adicione uma tarefa de Fluxo de Dados e, na superfície da guia **Fluxo de Dados** , crie um fluxo de dados para o manipulador de eventos. Para obter mais informações, consulte [Data Flow](data-flow/data-flow.md).  
  
9. No menu **Arquivo** , clique em **Salvar Itens Selecionados** para salvar o pacote.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Registro em Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md)  
  
  