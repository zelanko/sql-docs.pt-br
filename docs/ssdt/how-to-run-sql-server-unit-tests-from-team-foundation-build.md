---
title: Como executar testes de unidade do SQL Server no Team Foundation Build | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 24f5b85d-d6f9-415f-b09f-933b78dc0b67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe4b6dd462a8f8fec6797c26f7ae0461c4b0a4ce
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669855"
---
# <a name="how-to-run-sql-server-unit-tests-from-team-foundation-build"></a>Como: Executar testes de unidade do SQL Server no Team Foundation Build
Você pode usar o Team Foundation Build para executar os testes de unidade do SQL Server como parte de um teste de verificação da compilação (BVT). Você pode configurar os testes de unidade para implantar o banco de dados, gerar dados de teste e executar os testes selecionados. Se você não estiver familiarizado com o Team Foundation Build, analise as seguintes informações antes de seguir os procedimentos deste tópico:  
  
-   [Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
-   [Como configurar e executar testes agendados depois de criar seu aplicativo](https://msdn.microsoft.com/library/ms182465(VS.100).aspx)  
  
-   [Criar uma definição de build básica](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
  
Antes de executar esses procedimentos, primeiro você deve configurar o ambiente de trabalho realizando as seguintes tarefas:  
  
-   Instale o Team Foundation Build e o controle de versão do Team Foundation. Você provavelmente tem que instalar o Team Foundation Build e o controle de versão do Team Foundation em computadores diferentes.  
  
-   Instale o Microsoft SQL Server Data Tools Build Utilities no mesmo computador que o Team Foundation Build. Para instalar o SQL Server Data Tools Build Utilities, primeiro realize um ponto de instalação administrativo. Para saber mais sobre um ponto de instalação administrativo, confira [Instalar o SQL Server Data Tools](../ssdt/install-sql-server-data-tools.md). Em seguida, instale o SSDTBuildUtilties.msi no servidor de compilação do local (/location) usado para o ponto de instalação administrativo.  
  
-   Conecte-se a uma instância do Visual Studio Team Foundation Server.  
  
Após configurar o ambiente de trabalho, você deverá seguir estas etapas:  
  
1.  Crie um projeto de banco de dados.  
  
2.  Importe ou crie o esquema e os objetos do projeto de banco de dados.  
  
3.  Configure as propriedades do projeto de banco de dados para compilação e implantação.  
  
4.  Crie um ou mais testes de unidade.  
  
5.  Adicione a solução que contém o projeto de banco de dados e o projeto de teste de unidade para fazer o controle de versão e o check-in de todos os arquivos.  
  
Os procedimentos deste tópico descrevem como criar uma definição de compilação para executar os testes de unidade como parte de uma execução de teste automatizada:  
  
1.  [Definir configurações de teste para executar testes de unidade de banco de dados em um agente de compilação x64](#ConfigureX64)  
  
2.  [Atribuir testes a uma categoria de teste (opcional)](#CreateATestList)  
  
3.  [Modificar o projeto de teste](#ModifyTestProject)  
  
4.  [Fazer check-in da solução](#CheckInTheTestList)  
  
5.  [Criar uma definição de build](#CreateBuildDef)  
  
6.  [Executar a nova definição de build](#RunBuild)  
  
**Executar testes de unidade do SQL Server em um computador de compilação**  
  
Quando você executar testes de unidade em um computador de compilação, possivelmente eles não serão capazes de localizar os arquivos de projeto de banco de dados (.sqlproj). Esse problema ocorre porque o arquivo app.config faz referência a esses arquivos usando caminhos relativos. Além de isso, os testes da unidade poderão apresentar falhar se não conseguirem encontrar a instância do SQL Server que você deseja usar para executar os testes de unidade. Esse problema poderá ocorrer se as cadeias de conexão armazenadas no arquivo app.config não forem válidas no computador de compilação.  
  
Para resolver esses problemas, determine uma seção de substituição no app.config que substitua o arquivo app.config por um arquivo de configuração específico do ambiente do Team Foundation Build. Para saber mais, confira [Modificar o Projeto de Teste](#ModifyTestProject) posteriormente neste tópico.  
  
## <a name="ConfigureX64"></a>Definir configurações de teste para executar testes de unidade do SQL Server em um Agente de Build x64  
Para que você possa executar os testes de unidade em um agente de compilação x64, defina as configurações de teste para alterar a plataforma do processo do host.  
  
#### <a name="to-specify-the-host-process-platform"></a>Para especificar a plataforma do processo do host  
  
1.  Abra a solução que contém o projeto de teste cujas configurações você deseja definir.  
  
2.  No **Gerenciador de Soluções**, na pasta **Itens de Solução**, clique duas vezes no arquivo **Local.testsettings**.  
  
    A caixa de diálogo **Configurações de Teste** é exibida.  
  
3.  Na lista, clique em **Hosts**.  
  
4.  No painel de detalhes, em **Plataforma do Processo do Host**, clique em **MSIL** para configurar os testes a serem executados em um agente de compilação x64.  
  
5.  Clique em **Aplicar**.  
  
## <a name="CreateATestList"></a>Atribuir testes a uma categoria de teste (opcional)  
Normalmente, ao criar uma definição de compilação para executar testes de unidade, você especifica uma ou mais categorias de teste. Todos os testes nas categorias especificadas são executados quando a compilação é executada.  
  
#### <a name="to-assign-tests-to-a-test-category"></a>Para atribuir testes a uma categoria de teste  
  
1.  Abra a janela **Modo de Teste**.  
  
2.  Selecione um teste.  
  
3.  No painel de propriedades, clique em **Categorias de Teste** e clique nas reticências (…) na coluna da extrema direita.  
  
4.  Na janela **Categoria de Teste**, na caixa **Adicionar Nova Categoria**, digite um nome para a nova categoria de teste.  
  
5.  Clique em **Adicionar** e em **OK**.  
  
    A nova categoria de teste será atribuída ao teste e estará disponível para outros testes através de suas propriedades.  
  
## <a name="ModifyTestProject"></a>Modificar o projeto de teste  
Por padrão, o Team Foundation Build cria um arquivo de configuração no arquivo app.config do projeto ao criar o projeto de testes de unidade. O caminho para o projeto de banco de dados é armazenado como um caminho relativo no arquivo app.config. Os caminhos relativos que funcionam no Visual Studio não funcionarão, pois o Team Foundation Build coloca os arquivos compilados em locais diferentes, de acordo com o local em que você executou os testes de unidade. Além de isso, o arquivo app.config contém as cadeias de conexão que especificam o banco de dados a ser testado. Você também precisará de um arquivo app.config separado para o Team Foundation Build se o teste de unidade precisar se conectar a um banco de dados que não seja o que você usou quando o projeto de teste foi criado. Fazendo as modificações no próximo procedimento, você poderá configurar o projeto de teste e o servidor de compilação de modo que o Team Foundation Build use uma configuração diferente.  
  
> [!IMPORTANT]  
> Você deve executar esse procedimento para cada projeto de teste (.vbproj ou .vsproj).  
  
#### <a name="to-specify-an-appconfig-file-for-team-foundation-build"></a>Para especificar um arquivo app.config para o Team Foundation Build  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no arquivo app.config e clique em **Copiar**.  
  
2.  Clique com o botão direito do mouse no projeto de teste e clique em **Colar**.  
  
3.  Clique com o botão direito do mouse no arquivo **Copy of app.config** e clique em Renomear.  
  
4.  Digite _BuildComputer_**.sqlunitttest.config** e pressione ENTER, em que *BuildComputer* é o nome do computador no qual o agente de build é executado.  
  
5.  Clique duas vezes em *BuildComputer.sqlunitttest.config*.  
  
    O arquivo de configuração é aberto no editor.  
  
6.  Altere o caminho relativo do arquivo .sqlproj file adicionando um nível de pasta para a pasta Sources e uma subpasta com o mesmo nome da solução. Por exemplo, se o arquivo de configuração contiver inicialmente a seguinte entrada:  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    Atualize o arquivo desta maneira:  
  
    ```  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database3\Database3.sqlproj"      Configuration="Debug" />  
    ```  
  
    Quando você terminar, o arquivo *BuildComputer*.sqlunitttest.config deverá ter esta aparência no Visual Studio 2010:  
  
    ```  
    <SqlUnitTesting_VS2010>  
        <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
            Configuration="Debug" />  
        <DataGeneration ClearDatabase="true" />  
        <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
        <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
            CommandTimeout="30" />  
    </SqlUnitTesting_VS2010>  
    ```  
  
    Ou, se você estiver usando o Visual Studio 2012:  
  
    ```  
    <SqlUnitTesting_VS2012>  
            <DatabaseDeployment DatabaseProjectFileName="..\..\..\Database4\Database4.sqlproj"  
                Configuration="Debug" />  
            <DataGeneration ClearDatabase="true" />  
            <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
            <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(localdb)\Projects;Initial Catalog=Database4;Integrated Security=True;Pooling=False"  
                CommandTimeout="30" />  
        </SqlUnitTesting_VS2012>  
    ```  
  
7.  Atualize o atributo ConnectionString de ExecutionContext e PrivilegedContext para especificar conexões com o banco de dados de destino no qual você deseja fazer a implantação.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
9. No Gerenciador de Soluções, clique duas vezes em app.config.  
  
10. No editor, para cada nó \<SqlUnitTesting_*VSVersion*>, adicione `AllowConfigurationOverride="true"`. Por exemplo:  
  
    ```  
    -- Update SqlUnitTesting_VS2010 node to:  
    <SqlUnitTesting_VS2010 AllowConfigurationOverride="true">   
  
    -- Update SqlUnitTesting_VS2012 node to:  
    <SqlUnitTesting_VS2012 AllowConfigurationOverride="true">  
    ```  
  
    Com essa alteração, você permitirá que o Team Foundation Build use o arquivo de configuração substituto criado.  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
    Em seguida, atualize Local.testsettings para incluir o arquivo de configuração personalizada.  
  
#### <a name="to-customize-localtestsettings-to-deploy-the-customized-configuration-file"></a>Para personalizar Local.testsettings para implantar o arquivo de configuração personalizada  
  
1.  No Gerenciador de Soluções, clique duas vezes em Local.testsettings.  
  
    A caixa de diálogo **Configurações de Teste** é exibida.  
  
2.  Na lista de categorias, clique em **Implantação**.  
  
3.  Marque a caixa de seleção **Habilitar implantação**.  
  
4.  Clique em **Adicionar Arquivo**.  
  
5.  Na caixa de diálogo **Adicionar Arquivos de Implantação**, especifique o arquivo *BuildComputer*.sqlunitttest.config que você criou.  
  
6.  Clique em **Aplicar**.  
  
7.  Clique em **Fechar**.  
  
8.  No menu **Arquivo** , clique em **Salvar Tudo**.  
  
    Em seguida, faça o check-in da solução para controle de versão.  
  
## <a name="CheckInTheTestList"></a>Fazer check-in da solução  
Neste procedimento, você faz o check-in de todos os arquivos da solução. Esses arquivos incluem o arquivo de metadados de teste da sua solução, que contém suas associações de categoria de teste e testes. Sempre que você adicionar, excluir, reorganize ou alterar o conteúdo dos teste, o arquivo de metadados de teste será atualizado automaticamente para refletir essas alterações.  
  
> [!NOTE]  
> Este procedimento descreverá as etapas se você estiver usando o controle de versão do Team Foundation Build. Se você estiver usando um software de controle de versão diferente, siga as etapas apropriadas para o software.  
  
#### <a name="to-check-in-the-solution"></a>Para fazer check-in da solução  
  
1.  Conecte-se a um computador que esteja executando o Team Foundation Build.  
  
    Para saber mais, confira [Usar o Source Control Explorer](https://msdn.microsoft.com/library/ms181370(VS.100).aspx).  
  
2.  Se sua solução ainda não estiver no controle do código-fonte, adicione-a a ele.  
  
    Para saber mais, confira [Adicionar um projeto ou solução ao controle de versão](https://msdn.microsoft.com/library/ms181374(VS.100).aspx).  
  
3.  Clique em **Exibir** e clique em **Check-ins Pendentes**.  
  
4.  Faça check-in de todos os arquivos da solução.  
  
    Para saber mais, confira [Fazer check-in das alterações pendentes](https://msdn.microsoft.com/library/ms181411(VS.100).aspx).  
  
    > [!NOTE]  
    > Você poderia ter um processo de equipe específico que determinasse como os testes automatizados são criados e gerenciados. Por exemplo, o processo pode exigir que você verifique a compilação localmente antes de fazer check-in desse código junto com os testes que serão executados nele.  
  
    Em **Gerenciador de Soluções**, um ícone de cadeado aparece ao lado de cada arquivo para indicar que ele foi verificado. Para saber mais, confira [Propriedades de pasta e arquivo de controle de versão do modo de exibição](https://msdn.microsoft.com/library/ms245468(VS.100).aspx).  
  
    Os testes estão disponíveis para o Team Foundation Build. Agora você pode criar uma definição de compilação que contenha os testes a serem executados.  
  
## <a name="CreateBuildDef"></a>Criar uma definição de build  
  
#### <a name="to-create-a-build-definition"></a>Para criar uma definição de compilação  
  
1.  No Team Explorer, clique no projeto de equipe, clique com o botão direito do mouse no nó **Compilações** e clique em **Nova Definição de Build**.  
  
    A janela **Nova Definição de Build** é exibida.  
  
2.  Em **Nome da definição de build**, digite o nome que você deseja usar para a definição de build.  
  
3.  Na barra de navegação, clique em **Padrões de Build**.  
  
4.  Em **Copiar saída da compilação para a seguinte pasta de descarte (caminho UNC; por exemplo \\\servidor\compartilhamento)**, especifique uma pasta para conter a saída da compilação.  
  
    Você pode especificar uma pasta compartilhada no computador local ou em qualquer local de rede no qual o processo de compilação terá permissões.  
  
5.  Na barra de navegação, clique em **Processo**.  
  
6.  No grupo **Obrigatório**, em **Itens a Serem Compilados**, clique no botão procurar (...).  
  
7.  Na caixa de diálogo **Editor de Lista do Projeto de Compilação**, clique em **Adicionar**.  
  
8.  Especifique o arquivo de solução (.sln) que você adicionou ao controle de versão anterior neste passo a passo e clique em **OK**.  
  
    A solução aparece na lista **Arquivos de projeto ou de solução a serem compilados**.  
  
9. Clique em **OK**.  
  
10. No grupo **Básico**, em **Testes Automatizados**, especifique os testes a serem executados. Por padrão, os testes contidos nos arquivos denominados *test\*.dll na solução serão executados.  
  
11. No menu **Arquivo**, clique em **Salvar**  *Nome do Projeto*.  
  
    Você criou uma definição de compilação. Em seguida, você modificará o projeto de teste.  
  
## <a name="RunBuild"></a>Executar a nova definição de build  
  
#### <a name="to-run-the-new-build-type"></a>Para executar o novo tipo de compilação  
  
1.  No Team Explorer, expanda o nó do projeto de equipe, expanda o nó Compilações, clique com o botão direito do mouse na definição de compilação que deseja executar e clique em Enfileirar Nova Compilação.  
  
    A caixa de diálogo **Enfileirar build {**_TeamProjectName_**}** é exibida com uma lista de todos os tipos de build existentes.  
  
2.  Se necessário, em **Definição de build**, clique na nova definição de build.  
  
3.  Confirme se os valores nos campos **Definição de build**, **Agente de build** e **Pasta de descarte deste build** são apropriados e clique em **Enfileirar**.  
  
    A guia **Enfileirado** de **Gerenciador de Compilações** é exibida. Para saber mais, confira [Gerenciar e exibir compilações concluídas (Visual Studio 2010)](https://msdn.microsoft.com/library/ms181730(VS.100).aspx) or [Gerenciar suas compilações no Gerenciador de Compilações (Visual Studio 2012)](https://msdn.microsoft.com/library/ms181732.aspx).  
  
## <a name="see-also"></a>Consulte Também  
[Executar testes de unidade do SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Criar uma definição de build básica](https://msdn.microsoft.com/library/ms181716(VS.100).aspx)  
[Enfileirar um build](https://msdn.microsoft.com/library/ms181722(VS.100).aspx)  
[Monitorar o andamento de uma compilação em execução](https://msdn.microsoft.com/library/ms181724(VS.100).aspx)  
  
