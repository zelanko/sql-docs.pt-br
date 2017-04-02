---
title: "Assistente de Implanta&#231;&#227;o do Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.deploymentwizard.f1"
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Assistente de Implanta&#231;&#227;o do Integration Services
  O **Assistente de Implantação do Integration Services** dá suporte a dois modelos de implantação:
   - Modelo de implantação de projeto
   - Modelo de implantação do pacote 
   
 O **modelo de Implantação do Projeto** permite implantar um projeto do SSIS (SQL Server Integration Services) como uma única unidade no Catálogo do SSIS.
 
 O **modelo de Implantação do Pacote** permite implantar pacotes que você atualizou no Catálogo do SSIS sem precisar implantar o projeto todo. 
 
 > **OBSERVAÇÃO:** a implantação padrão do Assistente é o modelo de Implantação do Projeto.  
  
## Iniciar o assistente
Inicie o assistente:

 - Digitando **“Assistente de Implantação do SQL Server”** no Windows Search 

**OU**

 - Procurando o arquivo executável **ISDeploymentWizard.exe** na pasta de instalação do SQL Server; por exemplo: “C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn”. 
 
 > **OBSERVAÇÃO:** se a página **Introdução** for exibida, clique em **Avançar** para mudar para a página **Selecionar Fonte**. 
 
 As configurações nessa página são diferentes para cada modelo de implantação. Siga as etapas na seção [Project Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#ProjectModel) ou na seção [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) de acordo com o modelo selecionado nessa página.  
  
##  <a name="ProjectModel"></a> Modelo de Implantação do Projeto  
  
### Selecionar Origem  
 Para implantar um arquivo de implantação do projeto que você criou, selecione **Arquivo de implantação do projeto** e insira o caminho para o arquivo .ispac. Para implantar um projeto residente no catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , selecione **Catálogo do Integration Services**e insira o nome do servidor e o caminho para o projeto no catálogo. Clique em **Avançar** para ver a página **Selecionar Destino** .  
  
### Selecionar Destino  
 Para selecionar a pasta de destino para o projeto no catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , insira a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou clique em **Procurar** para selecionar de uma lista de servidores. Digite o caminho do projeto no SSISDB ou clique em **Procurar** para selecioná-lo. Clique em **Avançar** para ver a página **Revisar** .  
  
### Revisar (e implantar)  
 A página permite revisar as configurações que você selecionou. Você pode alterar suas seleções clicando em **Anterior**ou clicando em qualquer uma das etapas no painel esquerdo. Clique em **Implantar** para começar o processo de implantação.  
  
### Resultados  
 Depois que o processo de implantação estiver concluído, você deverá ver a página **Resultados** . Essa página exibe o êxito ou a falha de cada ação. Se a ação falhar, clique em **Com falha** na coluna **Resultado** para exibir uma explicação do erro. Clique em **Salvar Relatório...** para salvar os resultados em um arquivo XML ou clique em **Fechar** para sair do assistente.  
  
##  <a name="PackageModel"></a> Modelo de Implantação do Pacote  
  
### Selecionar Origem  
 A página **Selecionar Origem** no **Assistente de Implantação do Integration Services** mostra configurações específicas ao modelo de implantação do pacote quando você selecionou a opção **Implantação do Pacote** para o **modelo de implantação**.  
  
 Para selecionar os pacotes de origem, clique no botão **Procurar…** para selecionar a **pasta** that contains the packages or type the pasta path in the **Packages pasta path** e clique no botão **Atualizar** na parte inferior da página. Agora, você deve ver todos os pacotes na pasta especificada na caixa de listagem. Por padrão, todos os pacotes são selecionados. Clique na **caixa de seleção** na primeira coluna para escolher quais pacotes você quer que sejam implantados no servidor.  
  
 Consulte as colunas **Status** e **Mensagem** para verificar o status do pacote. Se o status estiver definido como **Pronto** ou **Aviso**, o assistente de implantação não bloqueará o processo de implantação. Ao passo que, se o status estiver definido como **Erro**, o assistente não continuará implantando os pacotes selecionados. Para exibir as mensagens de Aviso/Erro, clique no link na coluna **Mensagem**.  
  
 Se os dados confidenciais ou dados de pacote forem criptografados com uma senha, digite-a na coluna **Senha** e clique no botão **Atualizar** para verificar se ela é aceita. Se a senha estiver correta, o status mudará para **Pronto** e a mensagem de aviso desaparecerá. Se houver vários pacotes com a mesma senha, selecione os pacotes com a mesma senha de criptografia, digite a senha na caixa de texto **Senha** e clique no botão **Aplicar** . A senha deve ser aplicada aos pacotes selecionados.  
  
 Se o status de todos os pacotes selecionados não estiver definido como **Erro**, o botão **Avançar** será habilitado para que você possa continuar com o processo de implantação do pacote.  
  
### Selecionar Destino  
 Após seleção das origens do pacote, clique no botão **Avançar** para acessar a página **Selecionar Destino** . Os pacotes devem ser implantados em um projeto no Catálogo do SSIS (SSISDB). Portanto, antes de implantar pacotes, verifique se o projeto de destino já existe no Catálogo do SSIS. Caso contrário, crie um projeto vazio. Na página **Selecionar Destino** , digite o nome do servidor na caixa de texto **Nome do Servidor** ou clique no botão **Procurar…** para selecionar uma instância do servidor. Em seguida, clique no botão **Procurar…** ao lado da caixa de texto **Caminho** para especificar o projeto de destino. Se o projeto não existir, clique em **Novo projeto...** para criar um projeto vazio como o projeto de destino. O projeto **DEVE** ser criado em uma pasta.  
  
### Revisar e implantar  
 Clique em **Avançar** na página **Selecionar Destino** para acessar a página **Revisar** no **Assistente de Implantação do Integration Services**. Na página de revisão, revise o relatório de resumo sobre a ação de implantação. Depois da verificação, clique no botão **Implantar** para executar a ação de implantação.  
  
### Resultados  
 Depois que a implantação estiver concluída, você deverá ver a página **Resultados** . Na página **Resultados** , revise os resultados de cada etapa no processo de implantação. Na página **Resultados** , clique em **Salvar Relatório** para salvar o relatório de implantação ou em **Fechar** para fechar o assistente.  
  
## Consulte também  
 [Implantar projetos no Servidor do Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [Implantação de projetos e pacotes](https://msdn.microsoft.com/library/hh213290.aspx)  
  
  