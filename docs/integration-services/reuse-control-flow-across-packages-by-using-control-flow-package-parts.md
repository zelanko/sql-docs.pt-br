---
title: Reutilizar o fluxo de controle entre pacotes usando partes do pacote do fluxo de controle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.toolboxcontrolflowtemplate.f1
- sql13.dts.designer.addcopyexistingtemplate.f1
- sql13.dts.designer.addcopyexistingpackagepart.f1
- sql13.dts.designer.packagepart.general.f1
ms.assetid: 1edc91d9-1fab-4fe5-aed3-6f581fe32c18
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2fa693e4e5c8f21b9d8fc8ad02369bff7623b59e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295785"
---
# <a name="reuse-control-flow-across-packages-by-using-control-flow-package-parts"></a>Reutilizar o fluxo de controle entre pacotes usando partes do pacote do fluxo de controle

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Salve um contêiner ou tarefa de fluxo de controle frequentemente usado em um arquivo de parte autônomo, um arquivo ".dtsxp", e reutilize-o várias vezes em um ou mais pacotes usando as partes do pacote do fluxo de controle. Essa capacidade de reutilização facilita o desenvolvimento e manutenção dos pacotes do SSIS.  
  
## <a name="create-a-new-control-flow-package-part"></a>Criar uma nova parte do pacote do fluxo de controle  
 Para criar uma nova parte do pacote do fluxo de controle, no Gerenciador de Soluções, expanda a pasta **Partes do Pacote** . Clique com o botão direito do mouse em **Fluxo de Controle** e selecione **Nova Parte do Pacote do Fluxo de Controle**.  
  
 ![Criar um modelo de fluxo de controle](../integration-services/media/control-flow-templates-create-new.png "Criar um modelo de fluxo de controle")  
  
 Um novo arquivo de parte com a extensão “.dtsxp” é criado na pasta **Partes do Pacote | Fluxo de Controle** . Ao mesmo tempo, um novo item com o mesmo nome também é adicionado à caixa de ferramentas do SSIS. (Esse item de caixa de ferramentas só fica visível enquanto você tiver um projeto com a parte aberta no Visual Studio.)  
  
 ![Modelos de fluxo de controle na caixa de ferramentas](../integration-services/media/control-flow-templates-in-toolbox.png "Modelos de fluxo de controle na caixa de ferramentas")  
  
## <a name="design-a-control-flow-package-part"></a>Projetar uma nova parte do pacote do fluxo de controle  
 Para abrir o editor de parte do pacote, clique duas vezes no arquivo de parte no Gerenciador de Soluções. Você pode projetar a parte da mesma maneira que projeta um pacote.  
  
 ![Etapa 1 do design de modelo de fluxo de controle](../integration-services/media/control-flow-template-design-step-1.png "Etapa 1 do design de modelo de fluxo de controle")  
  
 ![Etapa 2 do design de modelo de fluxo de controle](../integration-services/media/control-flow-template-design-step-2.png "Etapa 2 do design de modelo de fluxo de controle")  
  
 As partes do pacote do fluxo de controle têm as seguintes limitações.  
  
-   Uma parte pode ter apenas um contêiner ou tarefa de nível superior. Se você quiser incluir várias tarefas ou contêineres, coloque-as em um contêiner de sequência única.  
  
-   Não é possível executar ou depurar uma parte diretamente no designer.  
  
## <a name="add-an-existing-control-flow-package-part-to-a-package"></a>Adicionar uma parte do pacote do fluxo de controle existente a um pacote  
 Você pode reutilizar partes salvas no projeto atual do Integration Services ou em um projeto diferente.  
  
-   Para reutilizar uma parte que faz parte do projeto atual, arraste e solte a parte da caixa de ferramentas.  
  
-   Para reutilizar uma parte que faz parte de um projeto diferente, use o comando **Adicionar parte do pacote do Fluxo de Controle existente** .  
  
### <a name="drag-and-drop-a-control-flow-package-part"></a>Arrastar e soltar uma parte do pacote do fluxo de controle  
 Para reutilizar uma parte em um projeto, basta arrastar e soltar o item da parte da caixa de ferramentas, assim como qualquer outra tarefa ou contêiner. Você pode arrastar e soltar a parte várias vezes em um pacote a fim de reutilizar a lógica em vários locais no pacote. Use esse método para reutilizar uma parte que faça parte do projeto atual.  
  
 ![Adicionar um modelo de fluxo de controle a um pacote](../integration-services/media/control-flow-templates-add-to-package.png "Adicionar um modelo de fluxo de controle a um pacote")  
  
 ![Pacote com vários modelos de fluxo de controle](../integration-services/media/control-flow-templates-in-package.png "Pacote com vários modelos de fluxo de controle")  
  
 Quando você salva o pacote, o designer do SSIS verifica se há qualquer instância da parte no pacote.  
  
-   Se o pacote contiver instâncias de parte, o designer gerará um novo arquivo .dtsx.designer contendo todas as informações relacionadas à parte.  
  
-   Se o pacote não usar partes, o designer excluirá qualquer arquivo .dtsx.designer criado anteriormente do pacote (ou seja, qualquer. arquivo .dtsx.designer que tenha o mesmo nome que o pacote).  
  
 ![Gerenciador de Soluções com modelos de fluxo de controle](../integration-services/media/control-flow-templates-in-solution-explorer.png "Gerenciador de Soluções com modelos de fluxo de controle")  
  
### <a name="add-a-copy-of-an-existing-control-flow-package-part-or-a-reference-to-an-existing-part"></a>Adicionar uma cópia de uma parte do pacote do fluxo de controle existente, ou uma referência a uma parte existente  
 Para adicionar uma cópia de uma parte existente no sistema de arquivos a um pacote, no Gerenciador de Soluções, expanda a pasta **Partes do Pacote** . Clique com o botão direito do mouse em **Fluxo de Controle** e selecione **Adicionar Parte do Pacote do Fluxo de Controle Existente**.  
  
 ![Adicionar um novo modelo de fluxo de controle no menu](../integration-services/media/control-flow-templates-add-from-menu.png "Adicionar um novo modelo de fluxo de controle no menu")  
  
 ![Caixa de diálogo Adicionar Cópia de Modelos Existentes](../integration-services/media/control-flow-templates-add-copy-dialog.png "Caixa de diálogo Adicionar Cópia de Modelos Existentes")  
  
 **Opções**  
  
 **Caminho da Parte do Pacote**  
 Digite o caminho para o arquivo da parte ou clique no botão Procurar (...) e localize o arquivo da parte para cópia ou referência.  
  
 **Adicionar como uma referência**  
 -   Se for selecionada, a parte será adicionada ao projeto do Integration Services como uma referência. Selecione esta opção quando você quiser fazer referência a uma única cópia de um arquivo de parte em vários projetos do Integration Services.  
  
-   Se for desmarcada, uma cópia do arquivo de parte será adicionada ao projeto.  
  
## <a name="configure-a-control-flow-package-part"></a>Configurar uma parte do pacote do fluxo de controle  
 Para configurar as partes do pacote do fluxo de controle depois de adicioná-las ao fluxo de controle de um pacote, use a caixa de diálogo **Configuração da Parte do Pacote**  .  
  
#### <a name="to-open-the-package-part-configuration-dialog-box"></a>Para abrir a caixa de diálogo Configuração da Parte do Pacote.  
  
1.  Para configurar uma instância de parte, clique duas vezes na instância da parte no fluxo de controle. Se preferir, clique com o botão direito do mouse na instância da parte e selecione **Editar**. A caixa de diálogo **Configuração da Parte do Pacote** é aberta.  
  
2.  Configure as propriedades e os gerenciadores de conexão para a instância da parte.  
  
### <a name="properties-tab"></a>Guia Propriedades  
 Use a guia **Propriedades** da caixa de diálogo **Configuração da Parte do Pacote**  para especificar as propriedades da parte.  
  
 ![Guia Propriedades da caixa de diálogo Configuração do Modelo](../integration-services/media/template-configuration-properties-tab.png "Guia Propriedades da caixa de diálogo Configuração do Modelo")  
  
 A hierarquia do modo de exibição de árvore no painel esquerdo lista todas as propriedades configuráveis da instância de parte.  
  
-   Se for desmarcada, a propriedade não será configurada na instância da parte. A instância da parte usa o valor padrão para a propriedade, que é definida na parte do pacote do fluxo de controle.  
  
-   Se for selecionado, o valor que você inserir ou selecionar substituirá o valor padrão.  
  
 A tabela no painel direito lista as propriedades para configuração.  
  
-   **Caminho da Propriedade**. O caminho de propriedade da propriedade.  
  
-   **Tipo de Propriedade**. O tipo de dados da propriedade.  
  
-   **Valor**. O valor configurado. Esse valor substitui o valor padrão.  
  
### <a name="connection-managers-tab"></a>Guia Gerenciadores de Conexões  
 Use a guia **Gerenciadores de Conexões** da caixa de diálogo **Configuração da Parte do Pacote**  para especificar as propriedades dos gerenciadores de conexões para a instância da parte.  
  
 ![Guia Gerenciadores de Conexões da caixa de diálogo Configuração do Modelo](../integration-services/media/template-configuration-connection-managers-tab.png "Guia Gerenciadores de Conexões da caixa de diálogo Configuração do Modelo")  
  
 A tabela no painel esquerdo lista todos os gerenciadores de conexão definidos na parte do fluxo de controle. Escolha o gerenciador de conexões que você deseja configurar.  
  
 A lista no painel direito relaciona as propriedades do gerenciador de conexões selecionado.  
  
-   **Definido**. Marcado se a propriedade for configurada para a instância da parte.  
  
-   **Nome da Propriedade**. O nome da propriedade.  
  
-   **Valor**. O valor configurado. Esse valor substitui o valor padrão.  
  
## <a name="delete-a-control-flow-part"></a>Excluir uma parte do fluxo de controle  
 Para excluir uma parte, no Gerenciador de Soluções, clique com o botão direito do mouse na parte e selecione **Excluir**. Escolha **OK** para confirmar a exclusão ou escolha **Cancelar** para manter a parte.  
  
 Se você excluir uma parte de um projeto, ele será excluído permanentemente do sistema de arquivos e não poderá ser restaurado.  
  
> [!NOTE]  
>  Se você quiser remover um pacote de um projeto do Integration Services, mas quiser continuar a usá-lo em outros projetos, use a opção **Excluir do Projeto**  em vez da opção **Excluir** .  
  
## <a name="package-parts-are-a-design-time-feature-only"></a>As partes do pacote são um recurso usado apenas no momento do design.  
 As partes do pacote são um recurso puramente do momento do design. O designer do SSIS cria, abre, salva e atualiza as partes e adiciona, configura ou exclui instâncias da parte em um pacote. No entanto, o runtime do SSIS não está ciente das partes. Veja como o designer consegue essa separação.  
  
-   O designer salva instâncias de parte do pacote com suas propriedades configuradas em um arquivo ".dtsx.designer".  
  
-   Quando o designer salva o arquivo ".dtsx.designer", ele também extrai o conteúdo das partes referenciadas por esse arquivo e substitui as instâncias da parte no pacote pelo conteúdo das partes.  
  
-   Por fim, todo o conteúdo, que não inclui mais informações sobre a parte, é salvo no arquivo de pacote ".dtsx". Esse é o arquivo executado pelo runtime do SSIS.  
  
 O diagrama a seguir demonstra a relação entre as partes (arquivos ".dtsxp"), o designer SSIS e o runtime do SSIS.  
  
 ![Fluxo e arquivos de modelos de fluxo de controle](../integration-services/media/control-flow-templates-intro.png "Fluxo e arquivos de modelos de fluxo de controle")  
  
  
