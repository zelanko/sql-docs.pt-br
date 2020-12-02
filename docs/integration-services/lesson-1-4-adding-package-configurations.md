---
description: Lição 1-4 – adicionar configurações de pacote
title: 'Etapa 4: adicionar configurações de pacote | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e04a5321-63d5-4ec5-85b9-cb4eaf6c87f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a1e2b55f3c61308d4f3dba30ac1c9b079031e01d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193804"
---
# <a name="lesson-1-4---adding-package-configurations"></a>Lição 1-4 – adicionar configurações de pacote

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Nessa tarefa, você adicionará uma configuração a cada pacote. As configurações atualizam os valores das propriedades e dos objetos do pacote em tempo de execução.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece uma variedade de tipos de configuração. Você pode armazenar configurações em variáveis de ambiente, entradas de Registro, variáveis definidas pelo usuário, tabelas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e arquivos XML. Para fornecer flexibilidade adicional, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] oferece suporte ao uso de configurações indiretas. Isso significa que você usa uma variável de ambiente para especificar o local da configuração, que por sua vez especifica os valores reais. Os pacotes no projeto Tutorial de Implantação usam uma combinação de arquivos de configuração XML e configurações indiretas. Um arquivo de configuração XML pode incluir configurações para várias propriedades e, quando apropriado, pode ser mencionado por vários pacotes. Neste tutorial, você usará um arquivo de configuração separado para cada pacote.  
  
Os arquivos de configuração normalmente contêm informações confidenciais, como cadeia de caracteres de conexão. Portanto, você deverá usar uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta em que você armazena os arquivos, e fornecer acesso apenas aos usuários ou contas com permissão para executar pacotes. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../integration-services/security/security-overview-integration-services.md#files).  
  
Os pacotes (DataTransfer e LoadXMLData) adicionados ao projeto Tutorial de Implantação na tarefa anterior precisam de configurações para serem executados com êxito depois de implantados no servidor de destino. Para implementar configurações, você criará primeiro as configurações indiretas para os arquivos XML e, depois, criará os arquivos de configuração XML.  
  
Serão criados dois arquivos de configuração, DataTransferConfig.dtsConfig e LoadXMLData.dtsConfig. Esses arquivos contêm os pares nome-valor que atualizam as propriedades nos pacotes que especificam o local dos arquivos de dados e de log usados pelo pacote. Depois, como uma etapa no processo de implantação, você atualizará os valores nos arquivos de configuração para refletir o novo local dos arquivos no computador de destino.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] reconhece que Datatransferconfig.dtsconfig e LoadXMLData.dtsConfig são dependências dos pacotes DataTransfer e LoadXMLData, e automaticamente incluirá os arquivos de configuração quando você criar o pacote de implantação na próxima lição.  
  
### <a name="to-create-indirect-configuration-for-the-datatransfer-package"></a>Para criar configuração indireta para o pacote DataTransfer  

Verifique o modelo de implantação atual do projeto e defina-o como **Modelo de Implantação de Pacote**, se necessário. No menu **Projeto**, clique em **Converter em Modelo de Implantação de Pacote**
  
1.  No Gerenciador de Soluções, clique duas vezes em DataTransfer.dtsx.  
  
2.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique em qualquer local no plano de fundo da superfície de design do fluxo de controle.  
  
3.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
4.  Na caixa de diálogo **Organizador de Configurações do Pacote**, selecione a opção **Habilitar configurações do pacote** , se não estiver selecionada, e clique em **Adicionar**.  
  
5.  Na página inicial do Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
6.  Na página Selecionar Tipo de Configuração, selecione **Arquivo de configuração XML** na lista **Tipo de configuração** , selecione a opção **O local de configuração está armazenado em uma variável do ambiente** e digite **DataTransfer** ou selecione a variável de ambiente **DataTransfer** na lista.  
  
    > [!NOTE]  
    > Para disponibilizar a variável de ambiente na lista, talvez você precise reiniciar o computador após a adição da variável. Se você não quiser reiniciar o computador, poderá digitar o nome da variável de ambiente.  
  
7.  Clique em **Próximo**.  
  
8.  Na página Concluindo o Assistente, digite **DataTransfer EV Configuration** na caixa **Nome da Configuração** , revise o conteúdo da configuração no painel **Visualização** e clique em **Concluir**.  
  
9. Feche a caixa de diálogo **Organizador de Configurações do Pacote**.  
  
### <a name="to-create-the-xml-configuration-for-the-datatransfer-package"></a>Para criar a configuração XML para o pacote DataTransfer  
  
1.  No Gerenciador de Soluções, clique duas vezes em DataTransfer.dtsx.  
  
2.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique em qualquer local no plano de fundo da superfície de design do fluxo de controle.  
  
3.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
4.  Na caixa de diálogo do Organizador de Configurações do Pacote, selecione a caixa de seleção **Habilitar Configurações do Pacote** e clique em **Adicionar**.  
  
5.  Na página inicial do Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
6.  Na página Selecionar Tipo de Configuração, selecione **Arquivo de configuração XML** na lista **Tipo de configuração** e clique em **Procurar**.  
  
7.  Na caixa de diálogo **Selecionar Local do Arquivo de Configuração** , procure C:\DeploymentTutorial, digite **DataTransferConfig** na caixa **Nome do arquivo** e clique em **Salvar**.  
  
8.  Na página Selecionar Tipo de Configuração, clique em **Avançar**.  
  
9. Na página Selecionar Propriedades a Serem Exportadas, expanda DataTransfer, Gerenciadores de Conexões, Log do Tutorial de Implantação e Propriedades e marque a caixa de seleção **Cadeia de Conexão** .  
  
10. Em Gerenciadores de Conexões, expanda NewCustomers e marque a caixa de seleção **Cadeia de Conexão** .  
  
11. Clique em **Próximo**.  
  
12. Na página Concluindo o Assistente, digite **DataTransfer Configuration** na caixa **Nome da configuração** , revise o conteúdo da configuração e clique em **Concluir**.  
  
13. Na caixa de diálogo **Organizador de Configurações do Pacote** , verifique se a opção DataTransfer EV Configuration é a primeira da lista e DataTransfer Configuration é a segunda da lista. Clique em **Fechar**.  
  
### <a name="to-create-indirect-configuration-for-the-loadxmldata-package"></a>Para criar configuração indireta para o pacote LoadXMLData  
  
1.  No Gerenciador de Soluções, clique duas vezes em LoadXMLData.dtsx.  
  
2.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique em qualquer local no plano de fundo da superfície de design do fluxo de controle.  
  
3.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
4.  Na caixa de diálogo **Organizador de Configurações do Pacote**, clique em **Adicionar**.  
  
5.  Na página inicial do Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
6.  Na página Selecionar Tipo de Configuração, selecione o **Arquivo de configuração XML** na lista **Tipo de configuração** , selecione a opção **O local de configuração está armazenado em uma variável do ambiente** , digite **LoadXMLData** ou selecione a variável de ambiente **LoadXMLData** na lista.  
  
    > [!NOTE]  
    > Para disponibilizar a variável de ambiente na lista, talvez você precise reiniciar o computador após a adição da variável.  
  
7.  Clique em **Próximo**.  
  
8.  Na página Concluindo o Assistente, digite **LoadXMLData EV Configuration** na caixa **Nome da configuração** , revise o conteúdo da configuração e clique em **Concluir**.  
  
### <a name="to-create-the-xml-configuration-for-the-loadxmldata-package"></a>Para criar a configuração XML para o pacote LoadXMLData  
  
1.  No Gerenciador de Soluções, clique duas vezes em LoadXMLData.dtsx.  
  
2.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique em qualquer local no plano de fundo da superfície de design do fluxo de controle.  
  
3.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
4.  Na caixa de diálogo do Organizador de Configurações do Pacote, marque a caixa de seleção **Habilitar Configurações do Pacote** e clique em **Adicionar**.  
  
5.  Na página inicial do Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
6.  Na página Selecionar Tipo de Configuração, selecione **Arquivo de configuração XML** na lista **Tipo de configuração** e clique em **Procurar**.  
  
7.  Na caixa de diálogo **Selecionar Local do Arquivo de Configuração** , procure C:\DeploymentTutorial, digite **LoadXMLDataConfig** na caixa **Nome do arquivo** e clique em **Salvar**.  
  
8.  Na página Selecionar Tipo de Configuração, clique em **Avançar**.  
  
9. Na página Selecionar Propriedades a Serem Exportadas, expanda LoadXMLData, Executáveis, Carregar Dados XML e Propriedades e marque as caixas de seleção **[XMLSource].[XMLData]** e **[XMLSource].[XMLSchemaDefinition]** .  
  
10. Clique em **Próximo**.  
  
11. Na página Concluindo o Assistente, digite **LoadXMLData Configuration** na caixa **Nome da configuração** , revise o conteúdo da configuração e clique em **Concluir**.  
  
12. Na caixa de diálogo **Organizador de Configurações do Pacote** , verifique se a opção LoadXMLData EV Configuration é a primeira da lista e LoadXMLData Configuration é a segunda da lista e clique em **Fechar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 5: Testar os pacotes atualizados](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="see-also"></a>Consulte Também  
[Configurações do Pacote](./packages/legacy-package-deployment-ssis.md)  
[Criar configurações de pacote](./packages/legacy-package-deployment-ssis.md)  
[Acesso aos arquivos usados por pacotes](../integration-services/security/security-overview-integration-services.md#files)