---
title: Criar configurações de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, configurations
- Package Configurations Organizer dialog box
- SSIS packages, configurations
- Integration Services packages, configurations
- configurations [Integration Services]
- packages [Integration Services], configurations
- deploying packages [Integration Services], configurations
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5bf5ca4c2e27f366a6f5ded97f9a9aa5213db122
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53361068"
---
# <a name="create-package-configurations"></a>Criar configurações de pacote
  Você cria as configurações do pacote por meio da caixa de diálogo **Organizador de Configurações do Pacote** e do Assistente de Configuração de Pacote. Para acessar essas ferramentas, clique em **Configurações do Pacote** no menu de **SSIS** em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Você também pode acessar o **Organizador de Configurações de Pacote** clicando no botão de reticências ao lado da propriedade **Configuração**. A propriedade Configuração aparece na janela de propriedades para o pacote.  
  
> [!NOTE]  
>  As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Na caixa de diálogo **Organizador de Configurações do Pacote** , você pode habilitar pacotes para usar configurações, adicionar e excluir configurações e definir a ordem de preferência para carregar as configurações.  
  
> [!NOTE]  
>  Quando as configurações de pacote são carregadas na ordem preferencial, elas são carregadas da parte superior da lista mostrada na caixa de diálogo **Organizador de Configurações do Pacote** até a parte inferior da lista. Porém, no tempo de execução, talvez as configurações do pacote não sejam carregadas na ordem preferencial. Em particular, as configurações do pacote pai são carregadas depois das configurações de outros tipos.  
  
> [!NOTE]  
>  Se várias configurações definirem a mesma propriedade de objeto, o valor carregado por último será usado no tempo de execução.  
  
 Na caixa de diálogo **Organizador de Configurações do Pacote** , você executa o Assistente de Configuração de Pacotes, que o guia através de etapas para criar uma configuração. Para executar o Assistente de Configuração de Pacotes, adicione uma nova configuração na caixa de diálogo **Organizador de Configurações do Pacote** ou edite uma existente. Nas páginas do assistente, você escolhe o tipo de configuração, escolhe se quer acessar a configuração diretamente ou usar variáveis de ambiente, e seleciona as propriedades a serem salvas na configuração.  
  
 O exemplo a seguir mostra as propriedades de destino de uma variável e de um pacote, do modo como são mostradas na página Concluindo o Assistente, no Assistente de Configuração de Pacotes:  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 Neste exemplo, a configuração atualiza estas propriedades:  
  
-   A propriedade RaiseChangedEvent da variável definida pelo usuário, `TodaysDate`.  
  
-   As propriedades MaximumErrorCount, LoggingMode e LocaleID do pacote.  
  
-   A propriedade Value da variável definida pelo usuário, `varTableName`, dentro do escopo da tarefa, My SQL Task.  
  
 O "\Package" representa a raiz e pontos (.) separam os objetos que definem o caminho até a propriedade que a configuração atualiza. Os nomes das variáveis e das propriedades estão entre parênteses. O termo Package sempre é usado na configuração, independente do nome do pacote; porém, todos os outros objetos no caminho usam os nomes definidos pelo usuário.  
  
 Depois que o assistente terminar, a nova configuração é adicionada à lista de configurações na caixa de diálogo **Organizador de Configurações do Pacote**.  
  
> [!NOTE]  
>  A última página do Assistente de Configuração de Pacote, Concluindo o Assistente, lista as propriedades de destino da configuração. Se quiser atualizar as propriedades enquanto estiver executando pacotes usando o utilitário prompt de comando **dtexec**, você poderá gerar as cadeias de caracteres que representam os caminhos de propriedade executando o Assistente de Configuração de Pacotes e, então, copiá-las e colá-las na janela do prompt de comando para usar com a opção definida de **dtexec.**  
  
 A tabela a seguir descreve as colunas da lista de configurações na caixa de diálogo **Organizador de Configurações do Pacote** .  
  
|coluna|Descrição|  
|------------|-----------------|  
|**Nome da Configuração**|O nome da configuração.|  
|**Tipo de Configuração**|O tipo de configuração.|  
|**Cadeia de Caracteres de Configuração**|O local da configuração. O local pode ser um caminho, uma variável de ambiente, uma chave do Registro, um nome de variável do pacote pai ou uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Objeto de Destino**|O nome do objeto com uma propriedade que tem uma configuração. Se a configuração for um arquivo de configuração XML, a coluna ficará em branco, devido à configuração poder atualizar vários objetos.|  
|**Propriedade de Destino**|O nome da propriedade. Se a configuração gravar em um arquivo de configuração XML ou em uma tabela do SQL Server, a coluna ficará em branco, pois a configuração pode atualizar vários objetos.|  
  
### <a name="to-create-a-package-configuration"></a>Para criar uma configuração de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)], clique na guia **Fluxo de Controle**, **Fluxo de Dados**, **Manipulador de Eventos** ou **Explorador de Pacotes**.  
  
4.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
5.  Na caixa de diálogo **Organizador de Configurações do Pacote** , selecione **Habilitar configurações do pacote**e clique em **Adicionar**.  
  
6.  Na página inicial da página Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
7.  Na página Selecionar Tipo de Configuração, especifique o tipo de configuração e defina as propriedades pertinentes ao tipo de configuração. Para obter mais informações, consulte [Referência da interface do usuário do Assistente de Configuração de Pacotes](../../2014/integration-services/package-configuration-wizard-ui-reference.md).  
  
8.  Na página Selecionar Propriedades a Serem Exportadas, selecione as propriedades dos objetos do pacote a serem incluídas na configuração. Se o tipo de configuração oferecer suporte somente a uma propriedade, o título dessa página de assistente será Selecionar Propriedade de Destino. Para obter mais informações, consulte [Referência da interface do usuário do Assistente de Configuração de Pacotes](../../2014/integration-services/package-configuration-wizard-ui-reference.md).  
  
    > [!NOTE]  
    >  Somente os tipos de configuração **Arquivo de Configuração XML** e **SQL Server** dão suporte à inclusão de várias propriedades em uma configuração.  
  
9. Na página Concluindo o Assistente, digite o nome da configuração e clique em **Concluir**.  
  
10. Exiba a configuração na caixa de diálogo **Organizador de Configurações do Pacote** .  
  
11. Clique em **Fechar**.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artigo técnico de [Noções básicas sobre configurações de pacotes do Integration Services](https://go.microsoft.com/fwlink/?LinkId=165643), em msdn.microsoft.com  
  
-   Entrada de blog [criando pacotes em código – configurações de pacote](https://go.microsoft.com/fwlink/?LinkId=217663), em www.sqlis.com.  
  
-   Entrada de blog [exemplo de API – adicione programaticamente um arquivo de configuração para um pacote](https://go.microsoft.com/fwlink/?LinkId=217664), em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Configurações do Pacote](../../2014/integration-services/package-configurations.md)   
 [Implantação de pacote &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)   
 [Trabalhar com variáveis programaticamente](building-packages-programmatically/working-with-variables-programmatically.md)  
  
  
