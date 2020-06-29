---
title: Usar os valores de variáveis e parâmetros em um pacote filho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- configurations [Integration Services]
- packages [Integration Services], configurations
- variables [Integration Services], adding
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a1ace15be59c7102547b4faedf70adc811bd140e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420193"
---
# <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a>Usar os valores de variáveis e parâmetros em um pacote filho
  Este procedimento descreve como criar uma configuração de pacote que usa o tipo de configuração variável pai. Este tipo de configuração habilita um pacote filho que é executado de um pacote pai para acessar uma variável no pai.  
  
> [!NOTE]  
>  Você também pode passar valores para um pacote filho configurando a tarefa Executar Pacote para mapear as variáveis de pacote pai ou parâmetros, ou parâmetros de projeto, para parâmetros de pacote filho. Para obter mais informações, consulte [Execute Package Task](control-flow/execute-package-task.md).  
  
 Não é necessário criar a variável no pacote pai antes de criar a configuração de pacote no pacote filho. É possível adicionar a variável ao pacote pai a qualquer momento, mas será preciso usar o nome exato da variável pai na configuração do pacote. Entretanto, antes de criar uma configuração da variável pai, é preciso que exista uma variável no pacote filho que possa ser atualizada pela configuração. Para obter mais informações sobre como adicionar e configurar variáveis, consulte [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
 O escopo da variável no pacote pai que é usado na configuração da variável pai pode ser definido como a tarefa Executar Pacote, tanto para o contêiner que tenha a tarefa quanto para o pacote. Se várias variáveis tiverem o mesmo nome, será usada a variável que tiver o escopo mais próximo da tarefa Executar Pacote. O escopo mais próximo da tarefa Executar Pacote é a própria tarefa.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>Adicionar uma variável a um pacote pai  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote no qual deseja adicionar uma variável para passar a um pacote filho.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , defina o escopo da variável, seguindo uma das ações:  
  
    -   Para definir o escopo para o pacote, clique na superfície de design da guia **Fluxo de Controle** .  
  
    -   Para definir o escopo para um contêiner pai da tarefa Executar Pacote, clique no contêiner.  
  
    -   Para definir o escopo da tarefa Executar Pacote, clique na tarefa.  
  
4.  Adicione e configure uma variável.  
  
    > [!NOTE]  
    >  Selecione um tipo de dados que seja compatível com os dados que serão armazenados pela variável.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-add-a-variable-to-a-child-package"></a>Adicionar uma variável a um pacote filho  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote no qual deseja adicionar uma configuração de variável pai.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer de [!INCLUDE[ssIS](../includes/ssis-md.md)] , defina o escopo para o pacote e clique na superfície de design da guia **Fluxo de Controle** .  
  
4.  Adicione e configure uma variável.  
  
    > [!NOTE]  
    >  Selecione um tipo de dados que seja compatível com os dados que serão armazenados pela variável.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-add-a-parent-package-configuration-to-a-child-package"></a>Adicionar uma configuração de pacote pai a um pacote filho  
  
1.  Se ainda não estiver aberto, abra o pacote filho no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique na superfície de design da guia **Fluxo de Controle** .  
  
3.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
4.  Na caixa de diálogo **Organizador de Configurações do Pacote** , selecione **Ativar configurações do pacote**e clique em **Adicionar**.  
  
5.  Na página inicial do Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
6.  Na página Selecionar Tipo de Configuração, na lista **Tipo de configuração** , selecione **Variável do pacote pai** e siga um dos seguintes procedimentos:  
  
    -   Selecione **Especificar as configurações de configuração diretamente**e na caixa **Variável pai** , forneça o nome da variável no pacote pai a ser usado na configuração.  
  
        > [!IMPORTANT]  
        >  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
    -   Selecione **O local de configuração está armazenado em uma variável do ambiente** e, na lista **Variável de ambiente**, selecione a variável de ambiente que contém o nome da variável.  
  
7.  Clique em **Avançar**.  
  
8.  Na página Selecionar Propriedade de Destino, expanda o nó **Variável** e o nó **Propriedades** da variável a ser configurada e, em seguida, clique na propriedade que será definida pela configuração.  
  
9. Clique em **Avançar**.  
  
10. Na página Concluindo o Assistente, você pode modificar o nome padrão da configuração e revisar a informações de configuração (opcional).  
  
11. Clique em **Concluir** para concluir o assistente e retornar para a caixa de diálogo **Organizador de Configurações do Pacote** .  
  
12. Na caixa de diálogo **Organizador de Configurações do Pacote** , a caixa **Configuração** lista a nova configuração.  
  
13. Clique em **fechar**  
  
## <a name="see-also"></a>Consulte Também  
 [Configurações do pacote](../../2014/integration-services/package-configurations.md)   
 [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md)   
 [Integration Services &#40;as variáveis&#41; SSIS](integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)  
  
  
