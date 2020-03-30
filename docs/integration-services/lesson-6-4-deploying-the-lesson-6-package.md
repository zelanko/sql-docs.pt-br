---
title: 'Etapa 4: Implantar pacote da Lição 6 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a16cd38eef12584f8d876e610bfda5d602c3076
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283021"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>Lição 6-4: Implantar o pacote da Lição 6

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Implantar o pacote envolve a adição do pacote no catálogo de SSISDB no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em uma instância do SQL Server. Nesta lição, você adicionará o pacote da Lição 6 no catálogo SSISDB, definirá o novo parâmetro e executará o pacote. Nesta lição, você usará o SQL Server Management Studio para adicionar o pacote da Lição 6 ao catálogo SSISDB e implantará esse pacote. Depois de implantar o pacote, você modificará o parâmetro para apontar para um novo local e, em seguida, executará o pacote.   
Nesta tarefa, você:  

1. Adicionar o pacote ao catálogo de SSISDB no nó SSIS no SQL Server.  
  
2. Implantar o pacote.  
  
3. Definir o valor de parâmetro do pacote.  

4. Executar o pacote no SSMS.  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>Localiza ou adiciona o catálogo do SSISDB  
  
1.  Selecione **Iniciar** > **Todos os Programas** > **Microsoft SQL Server 2017** e, em seguida, selecione **SQL Management Studio**.  
  
2.  Na caixa de diálogo **Conectar-se ao Servidor**, verifique as configurações padrão e selecione **Conectar**. Para se conectar, o nome do **Servidor** deve ser o nome do computador em que o SQL Server está instalado. Se o **Mecanismo de Banco de Dados** for uma instância nomeada, o nome do **Servidor** deverá ser o nome da instância no formato *\<nome_do_computador>\\\<nome_da_instância>* . 
  
3.  No **Pesquisador de Objetos**, expanda **Catálogos dos Integration Services**.  
  
4.  Se não houver nenhum catálogo listado em **Catálogos dos Integration Services**, adicione o catálogo SSISDB.  
  
5.  Para adicionar o catálogo do SSISDB, clique com o botão direito do mouse em **Catálogos dos Integration Services** e selecione **Criar Catálogo**.  
  
6.  Na caixa de diálogo **Criar Catálogo**, selecione **Habilitar a integração do CLR**.  
  
7.  Na caixa **Senha**, digite uma senha e, em seguida, insira-a novamente na caixa **Redigite a senha**. 
  
8.  Selecione **OK** para adicionar o catálogo SSISDB.  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>Adicionar o pacote ao catálogo SSISDB  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em **SSISDB** e selecione **Criar Pasta**.  
  
2.  Na caixa de diálogo **Criar Pasta**, insira Tutorial do SSIS na caixa de nome de pasta e selecione **OK**.  
  
3.  Expanda a pasta **Tutorial do SSIS**, clique com o botão direito do mouse em **Projetos** e selecione **Importar Pacotes**.  
  
4.  Na página **Introdução** do **Assistente de Conversão de Projeto do Integration Services**, selecione **Avançar**.  
  
5.  Na página **Localizar Pacotes**, verifique se o **Sistema de arquivos** está selecionado na lista de **Origem**; então, selecione **Procurar**.  
  
6.  Na caixa de diálogo **Procurar Pasta**, navegue até a pasta que contém o projeto do Tutorial do SSIS e selecione **OK**.  
  
7.  Selecione **Avançar**.  
  
8.  Na página Selecionar Pacotes, você deve ver todos os seis pacotes do Tutorial do SSIS. Na lista **Pacotes**, selecione **Lesson 6.dtsx** e selecione **Avançar**.  
  
9. Na página **Selecionar Destino**, insira **Implantação do Tutorial do SSIS** na caixa **Nome do Projeto** e selecione **Avançar**.

10. Selecione **Avançar** em cada uma das páginas restantes do assistente até chegar à página **Revisão**.  
  
11. Na página **Revisão**, selecione **Converter**.  
  
12. Depois que a conversão for concluída, selecione **Fechar**.  
  
Quando você fecha o Assistente de conversão de projeto do Integration Services, o SSIS exibe o Assistente de implantação do Integration Services. Você agora usará esse assistente para implantar o pacote da Lição 6.  
  
1.  Na página **Introdução** do **Assistente de Implantação do Integration Services**, examine as etapas de implantação do projeto e, em seguida, selecione **Avançar**.  
  
2.  Na página **Selecionar Destino**, verifique se o nome do servidor é a instância do SQL Server que contém o catálogo do SSISDB e o caminho mostra **Implantação do tutorial do SSIS**; então, selecione **Avançar**.  
  
3.  Na página **Revisão**, examine o **Resumo** e selecione **Implantar**.  
  
4.  Quando a implantação for concluída, selecione **Fechar**.  
  
5.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Catálogos do Integration Services** e selecione **Atualizar**.  
  
6.  Expanda **Catálogos do Integration Services** e então expanda **SSISDB**. Continue a expandir a árvore sob **Tutorial do SSIS** até ter expandido completamente o projeto. Você deve ver **Lesson 6.dtsx** no nó **Pacotes** do nó **Implantação do Tutorial do SSIS**.  
  
7.  Para verificar se o pacote está concluído, clique com o botão direito do mouse em **Lesson 6.dtsx** e clique em **Configurar**. Na caixa de diálogo **Configurar**, selecione **Parâmetros** e verifique se há uma entrada com **Lesson 6.dtsx** como o **Contêiner**, **VarFolderName** como o **Nome** e o caminho para **Novos Dados de Exemplo** como o valor e selecione **Fechar**.  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>Criar e popular uma nova pasta de dados de exemplo  
  
1.  No **Windows Explorer**, no nível da raiz da unidade (por exemplo, **C:\\** ), crie uma pasta chamada **Dados de Exemplo Dois**.  
  
2.  Abra a pasta **Dados de Exemplo** em [Pré-requisitos da Lição 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites) e copie qualquer um dos três dos arquivos de exemplo.  
  
3.  Navegue até a pasta **Dados de Exemplo Dois** e cole os arquivos copiados.  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>Alterar o parâmetro de pacote para apontar para os novos dados de exemplo  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Lesson 6.dtsx** e selecione **Configurar**.  
  
2.  Na caixa de diálogo **Configurar**, altere o valor do parâmetro para o caminho **Dados de Exemplo Dois**, por exemplo, **C:\\Dados de Exemplo Dois**.  
  
3.  Selecione **OK** para fechar a caixa de diálogo **Configurar**.  
  
## <a name="test-the-lesson-6-package-deployment"></a>Testar a implantação de pacote da Lição 6  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em **Lesson 6.dtsx** e selecione **Executar**.  
  
2.  Na caixa de diálogo **Executar Pacote**, selecione **OK**.  
  
3.  Na caixa de diálogo de mensagem, selecione **Sim** para abrir o **Relatório de Visão Geral**.  
  
O **Relatório de Visão Geral** para o pacote exibe o nome do pacote e um resumo de status. A seção **Visão Geral da Execução** mostra o resultado de cada tarefa no pacote. A seção **Parâmetros Usados** mostra os nomes e valores de todos os parâmetros usados na execução do pacote, incluindo **VarFolderName**.  
  
