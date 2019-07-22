---
title: Tarefa Fila de Mensagens | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.messagequeuetask.f1
- sql13.dts.designer.msgqueuetask.general.f1
- sql13.dts.designer.msgqueuetask.send.f1
- sql13.dts.designer.msgqueuetask.receive.f1
- sql13.dts.designer.selectvariables.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6cd6827a10bdacd11b092aa157b28604373aa018
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019664"
---
# <a name="message-queue-task"></a>Message Queue Task

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A Tarefa Fila de Mensagens permite usar o serviço de Enfileiramento de Mensagens (também conhecido como MSMQ) para enviar e receber mensagens entre pacotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou enviar mensagens a uma fila de aplicativos processada por um aplicativo personalizado. Essas mensagens podem adotar a forma de texto simples, arquivos ou variáveis e seus valores.  
  
 Usando a tarefa Fila de Mensagens, você pode coordenar operações em toda sua empresa. As mensagens podem ser enfileiradas e entregues mais tarde se o destino estiver indisponível ou ocupado; por exemplo, a tarefa pode enfileirar mensagens para o laptop offline de representantes de vendas que recebem suas mensagens quando se conectarem à rede. Você pode usar a tarefa Fila de Mensagens para os seguintes propósitos:  
  
-   Atrasar a execução da tarefa até que outros pacotes façam check-in. Por exemplo, depois de manutenção noturna em cada um de seus sites de varejo, uma tarefa Fila de Mensagens envia uma mensagem a seu computador corporativo. Um pacote que é executado no computador corporativo contém tarefas de Fila de Mensagens, cada uma esperando por uma mensagem de um site de varejo específico. Quando uma mensagem de um site chega, uma tarefa carrega dados daquele site. Depois que todos os sites fizerem check-in, o pacote computa os totais dos resumos.  
  
-   Enviando arquivos de dados ao computador que os processa. Por exemplo, a saída da caixa registradora de um restaurante pode ser enviada em uma mensagem de arquivo de dados ao sistema de folha de pagamento corporativo, onde os dados sobre as gorjetas de cada garçom são extraídos.  
  
-   Distribuindo arquivos para toda a sua empresa. Por exemplo, um pacote pode usar uma tarefa de Fila de Mensagens para enviar um arquivo de pacote a outro computador. Um pacote que é executado no computador de destino usa então uma tarefa de Fila de Mensagens para recuperar e salvar o pacote localmente.  
  
 Quando estiver enviando ou recebendo mensagens, a tarefa Fila de Mensagens usa um dos quatro tipos de mensagem: arquivo de dados, cadeia, mensagem de cadeia a variável, ou variável. O tipo de mensagem “mensagem de cadeia de caracteres para variável” só pode ser usada ao receber mensagens.  
  
 A tarefa usa um gerenciador de conexões MSMQ para se conectar à uma fila de mensagens. Para obter mais informações, consulte [Gerenciador de Conexão do SMO](../../integration-services/connection-manager/msmq-connection-manager.md). Para obter mais informações sobre o serviço de enfileiramento de mensagens, consulte a [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022).  
  
 A tarefa Fila de Mensagens requer que o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] esteja instalado. Alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode selecionar para instalação na página **Componentes a Serem Instalados** ou na página **Seleção de Recursos** do Assistente de Instalação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalam um subconjunto parcial de componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses componentes são úteis para tarefas específicas, mas a funcionalidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será limitada. Por exemplo, a opção [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] instala os componentes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessários para projetar um pacote, mas o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não é instalado e, portanto, a tarefa Fila de Mensagens não é funcional. Para assegurar uma instalação completa de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você deve selecionar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] na página **Componentes a Serem Instalados** . Para obter mais informações sobre como instalar e executar a tarefa Fila de Mensagens, consulte [Instalar o Integration Services](../../integration-services/install-windows/install-integration-services.md).  
  
> [!NOTE]  
>  A tarefa Fila de Mensagens não obedece ao Padrão Federal de Processamento de Informações (FIPS) 140-2 quando o sistema operacional do computador é configurado em modo FIPS e a tarefa usa criptografia. Se a tarefa Fila de Mensagens não usar criptografia, a tarefa poderá ser executada com êxito.  
  
## <a name="message-types"></a>Tipos de mensagem  
 Você pode configurar os tipos de mensagem que a tarefa Fila de Mensagens oferece dos seguintes modos:  
  
-   A mensagem**Data file** especifica que um arquivo contém a mensagem. Ao receber mensagens, você pode configurar a tarefa para gravar o arquivo, pode substituir um arquivo existente e pode especificar o pacote do qual a tarefa pode receber mensagens.  
  
-   A mensagem**String** especifica a mensagem como uma cadeia de caracteres. Ao receber mensagens, você pode configurar a tarefa para comparar a cadeia de caracteres recebida com uma cadeia de caracteres definida pelo usuário e entrar em ação dependendo da comparação. A comparação de cadeias de caracteres pode ser exata, diferenciar maiúsculas e minúsculas ou não diferenciar maiúsculas e minúsculas, ou usar uma subcadeia.  
  
-   **String message to variable** especifica a mensagem de fonte como uma cadeia de caracteres que é enviada a uma variável de destino. Você pode configurar a tarefa para comparar a cadeia de caracteres recebida com uma cadeia de caracteres definida pelo usuário usando uma comparação exata, que não pode diferenciar maiúsculas e minúsculas ou subcadeia. Esse tipo de mensagem só está disponível quando a tarefa estiver recebendo mensagens.  
  
-   **Variable** especifica que a mensagem contém uma ou mais variáveis. Você pode configurar a tarefa para especificar os nomes das variáveis incluídas na mensagem. Ao receber mensagens, você pode configurar a tarefa para especificar o pacote do qual ela pode receber mensagens e a variável que será o destino da mensagem.  
  
## <a name="sending-messages"></a>enviando mensagens  
 Ao configurar a tarefa Fila de Mensagens para enviar mensagens, você pode usar um dos algoritmos de criptografia que são atualmente suportados pela tecnologia de Serviço de enfileiramento de mensagens, RC2 e RC4, para criptografar a mensagem. Ambos esses algoritmos de criptografia são agora considerados criptograficamente fracos comparados a algoritmos mais novos que a tecnologia de Serviço de enfileiramento de mensagens ainda não aceita. Então, você deve considerar cuidadosamente suas necessidades de criptografia ao enviar mensagens que usam a tarefa Fila de Mensagens.  
  
## <a name="receiving-messages"></a>recebendo mensagens  
 Ao receber mensagens, a tarefa Fila de Mensagens pode ser configurada dos seguintes modos:  
  
-   Ignorar a mensagem ou remover a mensagem da fila.  
  
-   Especificar uma expiração.  
  
-   Falhar, se acontecer uma expiração.  
  
-   Substituir um arquivo existente, se a mensagem for armazenada em um **Data file**.  
  
-   Gravar o arquivo de mensagem com um nome de arquivo diferente, se a mensagem usar o tipo **Data file message** .  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>Mensagens de registro personalizadas disponíveis na tarefa Fila de Mensagens  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Fila de Mensagens. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**MSMQAfterOpen**|Indica que a tarefa finalizou a abertura da fila de mensagens.|  
|**MSMQBeforeOpen**|Indica que a tarefa começou a abrir a fila de mensagens.|  
|**MSMQBeginReceive**|Indica que a tarefa começou a receber uma mensagem.|  
|**MSMQBeginSend**|Indica que a tarefa começou a enviar uma mensagem.|  
|**MSMQEndReceive**|Indica que a tarefa terminou de receber uma mensagem.|  
|**MSMQEndSend**|Indica que a tarefa terminou de enviar uma mensagem.|  
|**MSMQTaskInfo**|Fornece informações descritivas sobre a tarefa.|  
|**MSMQTaskTimeOut**|Indica que o tempo limite da tarefa foi esgotado.|  
  
## <a name="configuration-of-the-message-queue-task"></a>Configuração da tarefa Fila de Mensagens  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte a documentação da classe **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** no Guia do Desenvolvedor.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou um contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="message-queue-task-editor-general-page"></a>Editor da Tarefa Fila de Mensagens (página Geral)
  Use a **página Geral** da caixa de diálogo do **Editor da Tarefa Fila de Mensagens** para nomear e descrever a tarefa Fila de Mensagens, especificar o formato da mensagem e indicar se a tarefa envia ou recebe mensagens.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Fila de Mensagens. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Fila de Mensagens.  
  
 **Use2000Format**  
 Indique se deseja usar o formato 2000 do serviço de enfileiramento de mensagens (também conhecido como MSMQ). O padrão é **False**.  
  
 **MSMQConnection**  
 Selecione um gerenciador de conexões de MSMQ existente ou clique em \<**Nova conexão...** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados**: [Gerenciador de conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md), [Editor do Gerenciador de conexões MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **Mensagem**  
 Especifique se a tarefa Fila de Mensagens envia ou recebe mensagens. Se você selecionar **Enviar mensagem**, será listada a página Enviar no painel esquerdo da caixa de diálogo; se você selecionar **Receber mensagem**, será listada a página Receber. Por padrão, esse valor está definido como **Enviar mensagem**.  
  
## <a name="message-queue-task-editor-send-page"></a>Editor da Tarefa Fila de Mensagens (página Enviar)
  Use a página **Enviar** da caixa de diálogo **Editor da Tarefa Fila de Mensagens** para configurar uma tarefa de Fila de Mensagens para enviar mensagens de um pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### <a name="options"></a>Opções  
 **UseEncryption**  
 Indique se a mensagem deve ser criptografada. O padrão é **False**.  
  
 **EncryptionAlgorithm**  
 Se você escolher usar criptografia, especifique o nome do algoritmo de criptografia a ser utilizado. A tarefa Fila de Mensagens pode usar os algoritmos RC2 e RC4. O padrão é **RC2**.  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. Na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
> [!IMPORTANT]  
>  Estes são os algoritmos de criptografia ao qual a tecnologia de serviço de Enfileiramento de Mensagens (também conhecido como MSMQ) oferece suporte. Atualmente, ambos algoritmos de criptografia são considerados criptograficamente fracos quando comparados a algoritmos mais novos, que não têm suporte no serviço de Enfileiramento de Mensagens. Então, você deve considerar cuidadosamente suas necessidades de criptografia ao enviar mensagens que usam a tarefa Fila de Mensagens.  
  
 **MessageType**  
 Selecione o tipo de mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Mensagem do arquivo de dados**|A mensagem é armazenada em um arquivo. Selecionar este valor faz com que seja exibida a opção dinâmica **DataFileMessage**.|  
|**Mensagem de variável**|A mensagem é armazenada em uma variável. Selecionar este valor faz com que seja exibida a opção dinâmica **VariableMessage**.|  
|**Mensagem de cadeia de caracteres**|A mensagem é armazenada em uma tarefa Fila de Mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
  
### <a name="messagetype-dynamic-options"></a>Opções dinâmicas de MessageType  
  
#### <a name="messagetype--data-file-message"></a>MessageType = Mensagem de arquivo de dados  
 **DataFileMessage**  
 Digite o caminho do arquivo de dados ou clique nas reticências **(…)** e localize o arquivo.  
  
#### <a name="messagetype--variable-message"></a>MessageType = Mensagem de variável  
 **VariableMessage**  
 Digite os nomes de variáveis ou clique nas reticências **(...)** e, em seguida, selecione as variáveis. As variáveis são separadas por vírgulas.  
  
 **Tópicos relacionados:** Selecionar variáveis  
  
#### <a name="messagetype--string-message"></a>MessageType = Mensagem de cadeia de caracteres  
 **StringMessage**  
 Digite a mensagem de cadeia de caracteres ou clique nas reticências **(...)** e digite a mensagem na caixa de diálogo **Inserir Mensagem de Cadeia de Caracteres**.  
  
## <a name="message-queue-task-editor-receive-page"></a>Editor da Tarefa Fila de Mensagens (página Receber)
  Use a página **Receber** da caixa de diálogo **Editor da Tarefa Fila de Mensagens** para configurar uma tarefa Fila de Mensagens para receber mensagens do MSMQ (Serviço de Enfileiramento de Mensagens) [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
### <a name="options"></a>Opções  
 **RemoveFromMessageQueue**  
 Indique se a mensagem deve ser removida da fila depois de ser recebida. Por padrão, esse valor é definido como **False**.  
  
 **ErrorIfMessageTimeOut**  
 Indique se a tarefa falha quando a mensagem expira, exibindo uma mensagem de erro. O padrão é **False**.  
  
 **TimeoutAfter**  
 Se você optar por exibir uma mensagem de erro quando uma tarefa falha, especifique quantos segundos esperar antes de ser exibida a mensagem de tempo limite ultrapassado.  
  
 **MessageType**  
 Selecione o tipo de mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Mensagem do arquivo de dados**|A mensagem é armazenada em um arquivo. Selecionar este valor faz com que seja exibida a opção dinâmica **DataFileMessage**.|  
|**Mensagem de variável**|A mensagem é armazenada em uma variável. Selecionar este valor faz com que seja exibida a opção dinâmica **VariableMessage**.|  
|**Mensagem de cadeia de caracteres**|A mensagem é armazenada em uma tarefa Fila de Mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
|**Mensagem de cadeia de caracteres para variável**|A mensagem<br /><br /> Selecionar este valor faz com que seja exibida a opção dinâmica **StringMessage**.|  
  
### <a name="messagetype-dynamic-options"></a>Opções dinâmicas de MessageType  
  
#### <a name="messagetype--data-file-message"></a>MessageType = Mensagem de arquivo de dados  
 **SaveFileAs**  
 Digite o caminho do arquivo a ser usado ou clique no botão de reticências **(...)** e, em seguida, localize o arquivo.  
  
 **Overwrite**  
 Indique se os dados em um arquivo existente devem ser substituídos quando o conteúdo de uma mensagem de arquivo de dados é salvo. O padrão é **False**.  
  
 **Filtro**  
 Especifique se deve ser aplicado um filtro à mensagem. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sem-filtro**|A tarefa não filtra as mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **IdentifierReadOnly**.|  
|**Do pacote**|A mensagem recebe somente mensagens do pacote especificado. Selecionar este valor faz com que seja exibida a opção dinâmica **Identifier**.|  
  
#### <a name="filter-dynamic-options"></a>Opções dinâmicas do filtro  
  
##### <a name="filter--no-filter"></a>Filtrar = Sem-filtro  
 **IdentifierReadOnly**  
 Esta opção é somente leitura. Pode ser em branco ou conter o GUID de um pacote quando a propriedade Filtrar tiver sido definida anteriormente.  
  
##### <a name="filter--from-package"></a>Filtrar = Do pacote  
 **Identificador**  
 Se você escolher aplicar um filtro, digite o identificador exclusivo do pacote do qual mensagens podem ser recebidas ou clique no botão de reticências **(…)** e especifique o pacote.  
  
 **Tópicos relacionados:** [Selecionar um Pacote](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--variable-message"></a>MessageType = Mensagem de variável  
 **Filter**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sem-filtro**|A tarefa não filtra as mensagens. Selecionar este valor faz com que seja exibida a opção dinâmica **IdentifierReadOnly**.|  
|**Do pacote**|A mensagem recebe somente mensagens do pacote especificado. Selecionar este valor faz com que seja exibida a opção dinâmica **Identifier**.|  
  
 **Variável**  
 Digite o nome da variável ou clique em \<**Nova variável...** > e configure uma variável nova.  
  
 **Tópicos relacionados:** [Adicionar Variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="filter-dynamic-options"></a>Opções dinâmicas do filtro  
  
##### <a name="filter--no-filter"></a>Filtrar = Sem-filtro  
 **IdentifierReadOnly**  
 Esta opção fica em branco.  
  
##### <a name="filter--from-package"></a>Filtrar = Do pacote  
 **Identificador**  
 Se você escolher aplicar um filtro, digite o identificador exclusivo do pacote do qual mensagens podem ser recebidas ou clique no botão de reticências **(…)** e especifique o pacote.  
  
 **Tópicos relacionados:** [Selecionar um Pacote](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--string-message"></a>MessageType = Mensagem de cadeia de caracteres  
 **Comparar**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhum.**|As mensagens não são comparadas.|  
|**Correspondência exata**|As mensagens devem corresponder exatamente à cadeia de caracteres na opção **CompareString** .|  
|**Ignora maiúsculas e minúsculas**|A mensagem deve corresponder à cadeia de caracteres da opção **CompareString** , mas a comparação não diferencia maiúsculas e minúsculas.|  
|**Contendo**|A mensagem deve conter a cadeia de caracteres na opção **CompareString** .|  
  
 **CompareString**  
 A menos que a opção **Comparar** esteja definida como **Nenhum**, forneça a cadeia de caracteres com a qual a mensagem é comparada.  
  
#### <a name="messagetype--string-message-to-variable"></a>MessageType = Mensagem de cadeia de caracteres para variável  
 **Comparar**  
 Especifique se deve ser aplicado um filtro às mensagens. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nenhum.**|As mensagens não são comparadas.|  
|**Correspondência exata**|A mensagem deve corresponder exatamente à cadeia de caracteres na opção **CompareString** .|  
|**Ignora maiúsculas e minúsculas**|A mensagem deve corresponder à cadeia de caracteres da opção **CompareString** , mas a comparação não diferencia maiúsculas e minúsculas.|  
|**Contendo**|A mensagem deve conter a cadeia de caracteres na opção **CompareString** .|  
  
 **CompareString**  
 A menos que a opção **Comparar** esteja definida como **Nenhum**, forneça a cadeia de caracteres com a qual a mensagem é comparada.  
  
 **Variável**  
 Digite o nome da variável para manter a mensagem recebida ou clique em \<**Nova variável...** > e configure uma variável nova.  
  
 **Tópicos relacionados:** [Adicionar Variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="select-variables"></a>Selecionar variáveis
  Use a caixa de diálogo **Selecionar Variáveis** para especificar as variáveis a serem usadas em uma operação de envio de mensagem na tarefa Fila de Mensagens. A lista das **Variáveis Disponíveis** inclui variáveis do sistema e aquelas definidas por usuários que estão no escopo da tarefa Fila de Mensagens ou no seu contêiner pai. A tarefa usa as variáveis da lista de **Variáveis Selecionadas** .  
  
### <a name="options"></a>Opções  
 **Variáveis Disponíveis**  
 Selecione uma ou mais variáveis.  
  
 **Variáveis Selecionadas**  
 Selecione uma ou mais variáveis.  
  
 **Setas à Direita**  
 Mova as variáveis selecionadas para a lista das **Variáveis Selecionadas** .  
  
 **Setas à esquerda**  
 Mova as variáveis selecionadas de volta para a lista das **Variáveis Selecionadas** .  
  
 **Nova Variável**  
 Crie uma nova variável.  
  
 **Tópicos relacionados:** [Adicionar Variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
