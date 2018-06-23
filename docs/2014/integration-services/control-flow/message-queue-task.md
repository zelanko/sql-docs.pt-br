---
title: Tarefa Fila de Mensagens | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.messagequeuetask.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3be2c48f2a3b2dc552d3f9c89bf2caf57b0e0bf4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010491"
---
# <a name="message-queue-task"></a>Message Queue Task
  A Tarefa Fila de Mensagens permite usar o serviço de Enfileiramento de Mensagens (também conhecido como MSMQ) para enviar e receber mensagens entre pacotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou enviar mensagens a uma fila de aplicativos processada por um aplicativo personalizado. Essas mensagens podem adotar a forma de texto simples, arquivos ou variáveis e seus valores.  
  
 Usando a tarefa Fila de Mensagens, você pode coordenar operações em toda sua empresa. As mensagens podem ser enfileiradas e entregues mais tarde se o destino estiver indisponível ou ocupado; por exemplo, a tarefa pode enfileirar mensagens para o laptop offline de representantes de vendas que recebem suas mensagens quando se conectarem à rede. Você pode usar a tarefa Fila de Mensagens para os seguintes propósitos:  
  
-   Atrasar a execução da tarefa até que outros pacotes façam check-in. Por exemplo, depois de manutenção noturna em cada um de seus sites de varejo, uma tarefa Fila de Mensagens envia uma mensagem a seu computador corporativo. Um pacote que é executado no computador corporativo contém tarefas de Fila de Mensagens, cada uma esperando por uma mensagem de um site de varejo específico. Quando uma mensagem de um site chega, uma tarefa carrega dados daquele site. Depois que todos os sites fizerem check-in, o pacote computa os totais dos resumos.  
  
-   Enviando arquivos de dados ao computador que os processa. Por exemplo, a saída da caixa registradora de um restaurante pode ser enviada em uma mensagem de arquivo de dados ao sistema de folha de pagamento corporativo, onde os dados sobre as gorjetas de cada garçom são extraídos.  
  
-   Distribuindo arquivos para toda a sua empresa. Por exemplo, um pacote pode usar uma tarefa de Fila de Mensagens para enviar um arquivo de pacote a outro computador. Um pacote que é executado no computador de destino usa então uma tarefa de Fila de Mensagens para recuperar e salvar o pacote localmente.  
  
 Quando estiver enviando ou recebendo mensagens, a tarefa Fila de Mensagens usa um dos quatro tipos de mensagem: arquivo de dados, cadeia, mensagem de cadeia a variável, ou variável. O tipo de mensagem “mensagem de cadeia de caracteres para variável” só pode ser usada ao receber mensagens.  
  
 A tarefa usa um gerenciador de conexões MSMQ para se conectar à uma fila de mensagens. Para obter mais informações, consulte [Gerenciador de Conexão do SMO](../connection-manager/msmq-connection-manager.md). Para obter mais informações sobre o serviço de enfileiramento de mensagens, consulte a [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=7022).  
  
 A tarefa Fila de Mensagens requer que o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esteja instalado. Alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode selecionar para instalação na página **Componentes a Serem Instalados** ou na página **Seleção de Recursos** do Assistente de Instalação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalam um subconjunto parcial de componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses componentes são úteis para tarefas específicas, mas a funcionalidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será limitada. Por exemplo, a opção [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] instala os componentes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessários para projetar um pacote, mas o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não é instalado e, portanto, a tarefa Fila de Mensagens não é funcional. Para assegurar uma instalação completa de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você deve selecionar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] na página **Componentes a Serem Instalados** . Para obter mais informações sobre como instalar e executar a tarefa Fila de Mensagens, consulte [Instalar o Integration Services](../install-windows/install-integration-services.md).  
  
> [!NOTE]  
>  A tarefa Fila de Mensagens não obedece ao Padrão Federal de Processamento de Informações (FIPS) 140-2 quando o sistema operacional do computador é configurado em modo FIPS e a tarefa usa criptografia. Se a tarefa Fila de Mensagens não usar criptografia, a tarefa poderá ser executada com êxito.  
  
## <a name="message-types"></a>Tipos de mensagem  
 Você pode configurar os tipos de mensagem que a tarefa Fila de Mensagens oferece dos seguintes modos:  
  
-   `Data file` mensagem especifica que um arquivo contém a mensagem. Ao receber mensagens, você pode configurar a tarefa para gravar o arquivo, pode substituir um arquivo existente e pode especificar o pacote do qual a tarefa pode receber mensagens.  
  
-   `String` mensagem especifica a mensagem como uma cadeia de caracteres. Ao receber mensagens, você pode configurar a tarefa para comparar a cadeia de caracteres recebida com uma cadeia de caracteres definida pelo usuário e entrar em ação dependendo da comparação. A comparação de cadeias de caracteres pode ser exata, diferenciar maiúsculas e minúsculas ou não diferenciar maiúsculas e minúsculas, ou usar uma subcadeia.  
  
-   `String message to variable` Especifica a mensagem de origem como uma cadeia de caracteres que é enviada a uma variável de destino. Você pode configurar a tarefa para comparar a cadeia de caracteres recebida com uma cadeia de caracteres definida pelo usuário usando uma comparação exata, que não pode diferenciar maiúsculas e minúsculas ou subcadeia. Esse tipo de mensagem só está disponível quando a tarefa estiver recebendo mensagens.  
  
-   `Variable` Especifica que a mensagem contém uma ou mais variáveis. Você pode configurar a tarefa para especificar os nomes das variáveis incluídas na mensagem. Ao receber mensagens, você pode configurar a tarefa para especificar o pacote do qual ela pode receber mensagens e a variável que será o destino da mensagem.  
  
## <a name="sending-messages"></a>enviando mensagens  
 Ao configurar a tarefa Fila de Mensagens para enviar mensagens, você pode usar um dos algoritmos de criptografia que são atualmente suportados pela tecnologia de Serviço de enfileiramento de mensagens, RC2 e RC4, para criptografar a mensagem. Ambos esses algoritmos de criptografia são agora considerados criptograficamente fracos comparados a algoritmos mais novos que a tecnologia de Serviço de enfileiramento de mensagens ainda não aceita. Então, você deve considerar cuidadosamente suas necessidades de criptografia ao enviar mensagens que usam a tarefa Fila de Mensagens.  
  
## <a name="receiving-messages"></a>recebendo mensagens  
 Ao receber mensagens, a tarefa Fila de Mensagens pode ser configurada dos seguintes modos:  
  
-   Ignorar a mensagem ou remover a mensagem da fila.  
  
-   Especificar uma expiração.  
  
-   Falhar, se acontecer uma expiração.  
  
-   Substituir um arquivo existente, se a mensagem for armazenada em um `Data file`.  
  
-   Salvar o arquivo de mensagem para um nome de arquivo diferente, se a mensagem usa o `Data file message` tipo.  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>Mensagens de registro personalizadas disponíveis na tarefa Fila de Mensagens  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Fila de Mensagens. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../custom-messages-for-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|`MSMQAfterOpen`|Indica que a tarefa finalizou a abertura da fila de mensagens.|  
|`MSMQBeforeOpen`|Indica que a tarefa começou a abrir a fila de mensagens.|  
|`MSMQBeginReceive`|Indica que a tarefa começou a receber uma mensagem.|  
|`MSMQBeginSend`|Indica que a tarefa começou a enviar uma mensagem.|  
|`MSMQEndReceive`|Indica que a tarefa terminou de receber uma mensagem.|  
|`MSMQEndSend`|Indica que a tarefa terminou de enviar uma mensagem.|  
|`MSMQTaskInfo`|Fornece informações descritivas sobre a tarefa.|  
|`MSMQTaskTimeOut`|Indica que o tempo limite da tarefa foi esgotado.|  
  
## <a name="configuration-of-the-message-queue-task"></a>Configuração da tarefa Fila de Mensagens  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor de tarefa da fila de mensagens &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de tarefa da fila de mensagens &#40;página receber&#41;](../message-queue-task-editor-receive-page.md)  
  
-   [Editor de tarefa da fila de mensagens &#40;Enviar página&#41;](../message-queue-task-editor-send-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte a documentação da classe **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** no Guia do Desenvolvedor.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou um contêiner](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas do Integration Services](integration-services-tasks.md)   
 [Fluxo de Controle](control-flow.md)  
  
  