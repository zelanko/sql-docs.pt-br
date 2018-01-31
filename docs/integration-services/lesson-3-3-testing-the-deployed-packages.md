---
title: 'Etapa 3: Testando os pacotes implantados | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 9159da3f-c9ca-4015-9e85-3bf4373a1349
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e51a4fb96520cd5a887fe27fb5eddd62062f4eae
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-3-3---testing-the-deployed-packages"></a>Lição 3-3 – Testando os pacotes implantados
Nesta tarefa, você testará os pacotes implantados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
Em outros tutoriais do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você executou pacotes no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], o ambiente de desenvolvimento do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], usando a opção **Iniciar Depuração** no menu **Depurar** . Desta vez você executará os pacotes de modo diferente.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece várias ferramentas que podem ser usadas para executar pacotes no ambiente de teste e de produção: o utilitário de prompt de comando **dtexec** e o Utilitário de Execução de Pacotes. O Utilitário do Pacote de Execução é uma ferramenta gráfica compilada no **dtexec**. Ambas as ferramentas executam o pacote imediatamente. Além disso, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece um subsistema do SQL Server Agent desenvolvido especialmente para agendar a execução do pacote como uma etapa em um trabalho do SQL Server Agent.  
  
Você usará o Utilitário do Pacote de Execução para executar os pacotes implantados. Os pacotes serão usados como estão; portanto, você não precisa atualizar as informações em nenhuma página na caixa de diálogo. Você executará os pacotes na página Geral, que é a primeira página do Utilitário do Pacote de Execução. Se preferir, também pode clicar em outras páginas para ver as informações que elas contêm para cada pacote.  
  
> [!NOTE]  
> Para garantir que os pacotes sejam executados com êxito no contexto desse tutorial, você não deve modificar nenhuma opção.  
  
Antes de executar os pacotes no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usando o Utilitário do Pacote de Execução, verifique se o serviço Integration Services está sendo executado. O serviço Integration Services fornece suporte ao armazenamento e execução de pacotes. Se o serviço for interrompido, você não poderá se conectar ao [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] não listará os pacotes a serem executados. Você também deve ter permissões para executar o pacote na instância em que o pacote foi implantado. Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../integration-services/security/integration-services-roles-ssis-service.md).  
  
As pastas de nível superior dentro da pasta Pacotes Armazenados são as pastas definidas pelo usuário que o serviço Integration Services monitora. Você pode especificar o número de pastas que quiser no arquivo MsDtsSrvr.ini.xml. Esse tutorial assume que você está usando o arquivo padrão MsDtsSrvr.ini.xml, e que os nomes das pastas de nível superior dos Pacotes Armazenados são Sistema de Arquivos e MSDB.  
  
### <a name="to-connect-to-integration-services-in-sql-server-management-studio"></a>Para se conectar ao Integration Services no SQL Server Management Studio  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , selecione **Integration Services** na lista **Tipo de servidor** , forneça um nome de servidor na caixa **Nome do servidor** e clique em **Conectar**.  
  
    > [!IMPORTANT]  
    > Se você não consegue se conectar ao [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], provavelmente o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não está sendo executado. Para saber o status do serviço, clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**. No painel esquerdo, clique em **Serviços do SQL Server**. No painel direito, localize o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Inicie o serviço se ainda não estiver em execução.  
  
    [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é aberto. Por padrão, a janela Pesquisador de Objetos é aberta e colocada no canto superior direito do estúdio. Se o Pesquisador de Objetos não for aberto, clique em **Pesquisador de Objetos** no menu **Exibir** .  
  
### <a name="to-run-the-packages-using-the-execute-package-utility"></a>Para executar os pacotes usando o Utilitário do Pacote de Execução  
  
1.  No Pesquisador de Objetos, expanda a pasta Pacotes Armazenados.  
  
2.  Expanda a pasta MSDB. Como você implantou os pacotes no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], todos os pacotes implantados serão armazenados no banco de dados msdb do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e todos os pacotes implantados serão exibidos na pasta MSDB. A pasta Sistema de Arquivos está vazia, a menos que você tenha implantado pacotes no sistema de arquivos fora do Tutorial de Implantação.  
  
3.  Começando no início da lista de pacotes, clique com o botão direito do mouse em DataTransfer e clique em **Executar Pacote**.  
  
4.  Na caixa de diálogo **Utilitário do Pacote de Execução** , clique em **Executar**.  
  
5.  Na caixa de diálogo **Utilitário do Pacote de Execução** , visualize os resultados de progresso e execução do pacote. Quando o botão **Parar** ficar indisponível, o que indica que o pacote está concluído, clique em **Fechar**.  
  
    > [!IMPORTANT]  
    > Se você clicar em **Parar** enquanto o pacote estiver sendo executado, o pacote não será concluído.  
  
6.  Na caixa de diálogo **Utilitário do Pacote de Execução** , clique em **Fechar**.  
  
7.  Repita as etapas de 3 a 6 para o pacote LoadXML.  
  
8.  No menu **Arquivo** , clique em **Sair**.  
  
### <a name="to-verify-the-results-of-the-datatransfer-package"></a>Para verificar os resultados do pacote DataTransfer  
  
1.  Na barra de ferramentas do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique em **Nova Consulta**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , selecione **Mecanismo de Banco de Dados** na lista **Tipo de servidor** , forneça o nome do servidor no qual você instalou os pacotes do tutorial ou digite (local) na caixa **Nome do servidor** e selecione um modo de autenticação. Se estiver usando a Autenticação do SQL Server, forneça um nome de usuário e senha.  
  
3.  Clique em **Conectar**.  
  
4.  Na janela de consulta, digite ou cole a instrução SQL seguinte:  
  
    `USE AdventureWorks`  
  
    `SELECT * FROM HighIncomeCustomers`  
  
5.  Pressione **F5** ou clique no ícone Executar na barra de ferramentas.  
  
    A consulta retorna 31 linhas de dados. O resultado de retorno contém todas as linhas do arquivo de texto, Customers.txt, com valores maiores que 100.000 na coluna YearlyIncome.  
  
6.  Localize a pasta DeploymentTutorial, clique com o botão direito do mouse no arquivo XML de log, Log do Tutorial de Implantação e clique em **Abrir**. Você pode abrir o arquivo usando o Bloco de Notas ou o editor de texto/XML de sua escolha.  
  
### <a name="to-verify-the-results-of-the-loadxmldata-package"></a>Para verificar os resultados do pacote LoadXMLData  
  
1.  Na barra de ferramentas do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique em **Nova Consulta**.  
  
2.  Se for solicitado que você se conecte novamente, na caixa de diálogo **Conectar ao Servidor** , selecione **Mecanismo de Banco de Dados** na lista **Tipo de servidor** , forneça o nome do servidor no qual você instalou os pacotes do tutorial ou digite (local) na caixa **Nome do servidor** e selecione um modo de autenticação. Se estiver usando a Autenticação do SQL Server, forneça um nome de usuário e senha.  
  
3.  Clique em **Conectar**.  
  
4.  Na janela de consulta, digite ou cole a instrução SQL seguinte:  
  
    `USE AdventureWorks`  
  
    `SELECT * FROM OrderDatesByCountryRegion`  
  
5.  Pressione **F5** ou clique no ícone Executar na barra de ferramentas.  
  
    A consulta retorna 21 linhas de dados. O resultado de retorno consiste em linhas do arquivo de dados XML, orders.xml. Cada linha é um resumo por país/região; a linha lista o nome do país/região, o número de ordens de cada país/região e as datas das ordens mais antigas e mais recentes.  
  
## <a name="see-also"></a>Consulte Também  
[Utilitário dtexec](../integration-services/packages/dtexec-utility.md)  
  
  
  
