---
title: Assistente de conversão de projeto do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 252d8c44921db82cc634e17e1628f72f18a066e1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396360"
---
# <a name="integration-services-project-conversion-wizard"></a>Assistente de Conversão de Projeto do Integration Services
  O **Assistente de Conversão de Projeto do Integration Services** converte um projeto no modelo de implantação de projeto.  
  
> [!NOTE]  
>  Se o projeto contiver uma ou mais fontes de dados, as fontes de dados serão removidas quando a conversão de projeto estiver concluída. Para criar uma conexão com uma fonte de dados que pode ser compartilhada pelos pacotes no projeto, adicione um gerenciador de conexões no nível de projeto. Para obter mais informações, consulte [adicionar, excluir ou compartilhar um Gerenciador de Conexão em um pacote](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md).  
  
 **O que você deseja fazer?**  
  
-   [Abrir o Assistente de Conversão de Projeto do Integration Services](#open_dialog)  
  
-   [Definir opções na página Localizar Pacotes](#locate)  
  
-   [Definir opções na página Selecionar Pacotes](#selectPackages)  
  
-   [Definir opções na página Selecionar Destino](#destination)  
  
-   [Definir opções na página Especificar Propriedades do Projeto](#projectProperties)  
  
-   [Definir opções na página Atualizar a Tarefa Executar Pacote](#executePackage)  
  
-   [Definir opções na página Selecionar Configurações](#configurations)  
  
-   [Definir opções na página Criar Parâmetros](#createParameters)  
  
-   [Definir opções na página Configurar Parâmetros](#configureParameters)  
  
-   [Definir as opções na página Revisão](#review)  
  
-   [Definir as opções em Executar Conversão](#conversion)  
  
##  <a name="open_dialog"></a> Abrir o Assistente de Conversão de Projeto do Integration Services  
 Siga um destes procedimentos para abrir o **Assistente de Conversão de Projeto do Integration Services** .  
  
-   Abra o projeto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]e, no Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Converter em Modelo de Implantação de Projeto**.  
  
-   No Pesquisador de Objetos, no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], clique com o botão direito do mouse no nó **Projetos** e selecione **Importar Pacotes**.  
  
 Dependendo em se você executa o **Assistente de Conversão de Projeto do Integration Services** no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], o assistente executa tarefas de conversão diferentes. Para obter mais informações, consulte [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
##  <a name="locate"></a> Definir opções na página Localizar Pacotes  
  
> [!NOTE]  
>  A página **Localizar Pacotes** somente está disponível quando você executa o assistente de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 A opção a seguir é exibida na página quando você seleciona **Sistema de arquivos** na lista suspensa **Origem** . Selecione esta opção quando o pacote estiver no sistema de arquivos.  
  
 **Pasta**  
 Digite o caminho do pacote ou navegue para o pacote clicando em **Procurar**.  
  
 As opções a seguir são exibidas na página quando você seleciona **Repositório de Pacotes SSIS** na lista suspensa **Origem**. Para obter mais informações sobre o repositório de pacotes, consulte [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](service/package-management-ssis-service.md).  
  
 **Servidor**  
 Digite o nome do servidor ou selecione o servidor.  
  
 **Pasta**  
 Digite o caminho do pacote ou navegue para o pacote clicando em **Procurar**.  
  
 As opções a seguir são exibidas na página quando você seleciona **Microsoft SQL Server** na lista suspensa **Origem** . Selecione esta opção quando o pacote estiver no Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Servidor**  
 Digite o nome do servidor ou selecione o servidor.  
  
 **Usar a autenticação do Windows**  
 O modo de Autenticação do Microsoft Windows permite que um usuário se conecte por meio de uma conta de usuário do Windows. Se usar Autenticação do Windows, não será preciso fornecer um nome de usuário nem senha.  
  
 **Usar Autenticação do SQL Server**  
 Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autentica a conexão verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha registrada previamente. Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro.  
  
 **Nome de usuário**  
 Especifique um nome de usuário quando você estiver usando a Autenticação do SQL Server.  
  
 **Senha**  
 Forneça uma senha quando você estiver usando a Autenticação do SQL Server.  
  
 **Pasta**  
 Digite o caminho do pacote ou navegue para o pacote clicando em **Procurar**.  
  
##  <a name="selectPackages"></a> Definir opções na página Selecionar Pacotes  
 **Nome do Pacote**  
 Lista o arquivo do pacote.  
  
 **Status**  
 Indica se um pacote está pronto para ser convertido ao modelo de implantação de projeto.  
  
 **Mensagem**  
 Exibe uma mensagem associada ao pacote.  
  
 **Senha**  
 Exibe uma senha associada ao pacote. O texto da senha está oculto.  
  
 **Aplicar à seleção**  
 Clique para aplicar a senha na caixa de texto **Senha** , para o pacote ou pacotes selecionados.  
  
 **Atualizar**  
 Atualiza a lista de pacotes.  
  
##  <a name="destination"></a> Definir opções na página Selecionar Destino  
 Nessa página, especifique o nome e o caminho de um novo arquivo de implantação de projeto (.ispac) ou selecione um arquivo existente.  
  
> [!NOTE]  
>  A página **Selecionar destino** está disponível apenas quando você executa o assistente de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 **Caminho de saída**  
 Digite o caminho para o arquivo de implantação ou navegue para o arquivo clicando em **Procurar**.  
  
 **Nome do projeto**  
 Digite o nome do projeto.  
  
 **Nível de proteção**  
 Selecione o nível de proteção. Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descrição do projeto**  
 Digite uma descrição opcional para o projeto.  
  
##  <a name="projectProperties"></a> Definir opções na página Especificar Propriedades do Projeto  
  
> [!NOTE]  
>  A página **Especificar Propriedades do Projeto** está disponível apenas quando você executa o assistente de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Nome do projeto**  
 Lista o nome do projeto.  
  
 **Nível de proteção**  
 Selecione um nível de proteção para os pacotes contidos no projeto. Para obter mais informações sobre níveis de proteção, consulte [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descrição do projeto**  
 Digite uma descrição de projeto opcional.  
  
##  <a name="executePackage"></a> Definir opções na página Atualizar a Tarefa Executar Pacote  
 Atualizar as Tarefas Executar Pacote contidas nos pacotes, para usar uma referência baseada em projeto. Para obter mais informações, consulte [Execute Package Task Editor](../../2014/integration-services/execute-package-task-editor.md).  
  
 **Pacote pai**  
 Lista o nome do pacote que executa o pacote filho usando a tarefa Executar Pacote.  
  
 **Nome da tarefa**  
 Lista o nome da tarefa Executar Pacote.  
  
 **Referência original**  
 Lista o caminho atual do pacote filho.  
  
 **Atribuir referência**  
 Selecione um pacote filho armazenado no projeto.  
  
##  <a name="configurations"></a> Definir opções na página Selecionar Configurações  
 Selecione as configurações de pacote que você deseja substituir por parâmetros.  
  
 **Pacote**  
 Lista o arquivo do pacote.  
  
 **Tipo**  
 Lista o tipo de configuração, como um arquivo de configuração XML.  
  
 **Cadeia de Caracteres de Configuração**  
 Lista o caminho do arquivo de configuração.  
  
 **Status**  
 Exibe uma mensagem de status para a configuração. Clique na mensagem para exibir o texto inteiro da mensagem.  
  
 **Adicionar configurações**  
 Adicione configurações de pacote contidas em outros projetos à lista de configurações disponíveis que você deseja substituir por parâmetros. Você pode selecionar configurações armazenadas em um sistema de arquivos ou armazenados no SQL Server.  
  
 **Atualizar**  
 Clique para atualizar a lista de configurações.  
  
 **Remover configurações de todos os pacotes após a conversão**  
 É recomendável remover todas as configurações do projeto selecionando essa opção.  
  
 Se você não selecionar essa opção, somente as configurações selecionadas para substituir por parâmetros serão removidas.  
  
##  <a name="createParameters"></a> Definir opções na página Criar Parâmetros  
 Selecione o nome do parâmetro e o escopo para cada propriedade de configuração.  
  
 **Pacote**  
 Lista o arquivo do pacote.  
  
 **Nome do parâmetro**  
 Lista o nome do parâmetro.  
  
 **Escopo**  
 Selecione o escopo do parâmetro, pacote ou projeto.  
  
##  <a name="configureParameters"></a> Definir opções na página Configurar Parâmetros  
 **Nome**  
 Lista o nome do parâmetro.  
  
 **Escopo**  
 Lista o escopo do parâmetro.  
  
 **Value**  
 Lista o valor do parâmetro.  
  
 Clique no botão de reticências ao lado do campo de valor para configurar as propriedades do parâmetro.  
  
 Na caixa de diálogo **Definir Detalhes de Parâmetros** , edite o valor do parâmetro. Você também pode especificar se o valor do parâmetro deve ser fornecido quando você executar o pacote.  
  
 Você pode modificar o valor na página **Parâmetros** da caixa de diálogo **Configurar** no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], clique no botão Procurar ao lado do parâmetro. A caixa de diálogo **Definir Valor do Parâmetro** é exibida.  
  
 A caixa de diálogo **Definir Detalhes de Parâmetros** também lista o tipo de dados do valor de parâmetro e a origem do parâmetro.  
  
##  <a name="review"></a> Definir as opções na página Revisão  
 Use a página **Revisão** para confirmar as opções selecionadas para a conversão do projeto.  
  
 **Anterior**  
 Clique para alterar uma opção.  
  
 **Converter**  
 Clique para converter o projeto no modelo de implantação de projeto.  
  
##  <a name="conversion"></a> Definir as opções em Executar Conversão  
 A página Executar Conversão mostra o status da conversão do projeto.  
  
 **Ação**  
 Lista uma etapa de conversão específica.  
  
 **Resultado**  
 Lista o status de cada etapa de conversão. Clique na mensagem de status para obter mais informações.  
  
 A conversão de projeto não será salva até que o projeto seja salvo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Salvar relatório**  
 Clique para salvar um resumo da conversão de projeto em um arquivo .xml.  
  
## <a name="see-also"></a>Consulte também  
 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  
