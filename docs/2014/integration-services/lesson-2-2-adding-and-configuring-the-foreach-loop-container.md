---
title: 'Etapa 2: Adicionando e configurando o contêiner do Loop Foreach | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e07d71e77fc3de250ca01bb4e7fb2fb0bf15817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767518"
---
# <a name="step-2-adding-and-configuring-the-foreach-loop-container"></a>Etapa 2: Adicionar e configurar o contêiner Loop Foreach
  Nessa tarefa, você adicionará a capacidade de executar loop através de uma pasta de arquivos simples e aplicará a mesma transformação Fluxo de Dados usada na Lição 1 para cada um desses arquivos simples. Você faz isto adicionando e configurando um contêiner Loop Foreach ao fluxo de controle.  
  
 O contêiner Loop Foreach que você adicionar deve ser capaz de se conectar a cada arquivo simples na pasta. Como todos os arquivos da pasta têm o mesmo formato, o contêiner Loop Foreach pode usar o mesmo gerenciador de conexões de Arquivo Simples para conectar-se a cada um desses arquivos. O gerenciador de conexões de Arquivo Simples que o contêiner usará é o mesmo gerenciador de conexões de Arquivo Simples que você criou na Lição 1.  
  
 Atualmente, o gerenciador de conexões de Arquivo Simples da Lição 1 se conecta a um único arquivo simples específico. Para conectar-se iterativamente a cada arquivo simples da pasta, você terá que configurar o contêiner Loop Foreach e o gerenciador de conexões de Arquivo Simples da seguinte maneira:  
  
-   **Contêiner do Loop Foreach:** Você mapeará o valor enumerado do contêiner para uma variável de pacote definida pelo usuário. O contêiner usará a variável definida pelo usuário para modificar dinamicamente a propriedade `ConnectionString` do gerenciador de conexões de Arquivo Simples, e conectar-se iterativamente a cada um dos arquivos simples da pasta.  
  
-   **Gerenciador de conexões de Arquivo Simples:** Você modificará o Gerenciador de conexão que foi criado na lição 1 usando uma variável definida pelo usuário para popular o Gerenciador de conexão `ConnectionString` propriedade.  
  
 Os procedimentos nessa tarefa mostram como você pode criar e modificar o contêiner Loop Foreach para usar uma variável definida pelo usuário e adicionar a tarefa de fluxo de dados ao loop. Você aprenderá como modificar o gerenciador de conexões de Arquivo Simples para usar uma variável definida pelo usuário na próxima tarefa.  
  
 Após essas modificações no pacote, quando ele for executado, o contêiner Loop Foreach iterará através dessa coleção de arquivos na pasta Dados de Exemplo. Toda vez que um arquivo é encontrado e corresponde ao critério, o contêiner Loop Foreach irá popular a variável definida pelo usuário com o nome do arquivo, mapeará a variável definida pelo usuário para a propriedade `ConnectionString` do gerenciador de conexões do Arquivo Simples de Dados Moeda de exemplo e, então, executará o fluxo de dados naquele arquivo. Portanto, em cada iteração do Loop Foreach a tarefa de Fluxo de Dados consumirá um arquivo simples diferente.  
  
> [!NOTE]  
>  Como o [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa o fluxo de controle do fluxo de dados, qualquer loop que você adicionar ao fluxo de controle não exigirá modificações no fluxo de dados. Portanto, o fluxo de dados que você criou na Lição 1 não tem que ser alterado.  
  
### <a name="to-add-a-foreach-loop-container"></a>Para adicionar um contêiner Loop Foreach  
  
1.  Em **SQL Server Data Tools**, clique na guia **Fluxo de Controle** .  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Contêineres**e arraste um **Contêiner Loop Foreach** até a superfície de design da guia **Fluxo de Controle** .  
  
3.  Clique com o botão direito do mouse no **Contêiner Loop Foreach** recém-adicionado e selecione **Editar**.  
  
4.  No **Editor de Loop Foreach** caixa de diálogo a **gerais** página, para **nome**, digite `Foreach File in Folder`. Clique em **OK**.  
  
5.  O contêiner Foreach Loop com o botão direito, clique em **propriedades**e na janela Propriedades, verifique se o `LocaleID` estiver definida como **inglês (Estados Unidos)** .  
  
### <a name="to-configure-the-enumerator-for-the-foreach-loop-container"></a>Para configurar o enumerador para o contêiner Loop Foreach  
  
1.  Clique duas vezes em Arquivo Foreach na Pasta para abrir novamente o **Editor de Loop Foreach**.  
  
2.  Clique em **Coleção**.  
  
3.  Na página **Coleção** , selecione **Enumerador de Arquivo Foreach**.  
  
4.  No grupo **Configuração do enumerador** , clique em **Procurar**.  
  
5.  Na caixa de diálogo **Procurar pasta** , localize a pasta no computador que contém os arquivos Currency_*.txt.  
  
     Estes dados de exemplo estão incluídos com os pacotes de lição do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para baixar os dados de exemplo e os pacotes de lição, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no hiperlink "http://msftisprodsamples.codeplex.com/downloads/get/578097" SQL2012. Arquivo Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
6.  Na caixa **Arquivos**, digite **Currency_\*.txt**.  
  
### <a name="to-map-the-enumerator-to-a-user-defined-variable"></a>Para mapear o enumerador para uma variável definida pelo usuário  
  
1.  Clique em **Mapeamentos de Variáveis**.  
  
2.  Na página **Mapeamentos de Variáveis**, na coluna **Variável**, clique na célula vazia e selecione **\<Nova Variável...>** .  
  
3.  No **Adicionar variável** caixa de diálogo, para **nome**, tipo `varFileName`.  
  
    > [!IMPORTANT]  
    >  Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
4.  Clique em **OK**.  
  
5.  Clique em **OK** novamente para sair da caixa de diálogo **Editor de Loop Foreach** .  
  
### <a name="to-add-the-data-flow-task-to-the-loop"></a>Para adicionar a tarefa de fluxo de dados ao loop  
  
-   Arraste o **extrair dados de moeda de exemplo** tarefa de fluxo de dados para o contêiner Foreach Loop agora renomeado `Foreach File in Folder`.  
  
## <a name="next-lesson-task"></a>Próxima tarefa da lição  
 [Etapa 3: Modificando o gerenciador de conexões de arquivo simples](lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>Consulte também  
 [Para configurar um contêiner Loop Foreach](control-flow/foreach-loop-container.md)   
 [Usar variáveis em pacotes](use-variables-in-packages.md)  
  
  
