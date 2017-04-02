---
title: "Etapa 2: adicionando e configurando o cont&#234;iner Loop Foreach | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Etapa 2: adicionando e configurando o cont&#234;iner Loop Foreach
Nessa tarefa, você adicionará a capacidade de executar loop através de uma pasta de arquivos simples e aplicará a mesma transformação Fluxo de Dados usada na Lição 1 para cada um desses arquivos simples. Você faz isto adicionando e configurando um contêiner Loop Foreach ao fluxo de controle.  
  
O contêiner Loop Foreach que você adicionar deve ser capaz de se conectar a cada arquivo simples na pasta. Como todos os arquivos da pasta têm o mesmo formato, o contêiner Loop Foreach pode usar o mesmo gerenciador de conexões de Arquivo Simples para conectar-se a cada um desses arquivos. O gerenciador de conexões de Arquivo Simples que o contêiner usará é o mesmo gerenciador de conexões de Arquivo Simples que você criou na Lição 1.  
  
Atualmente, o gerenciador de conexões de Arquivo Simples da Lição 1 se conecta a um único arquivo simples específico. Para conectar-se iterativamente a cada arquivo simples da pasta, você terá que configurar o contêiner Loop Foreach e o gerenciador de conexões de Arquivo Simples da seguinte maneira:  
  
-   **Contêiner Loop Foreach:** você mapeará o valor enumerado do contêiner para uma variável de pacote definida pelo usuário. O contêiner usará a variável definida pelo usuário para modificar dinamicamente a propriedade **ConnectionString** do gerenciador de conexões de Arquivo Simples e conectar-se de forma iterativa a cada um dos arquivos simples da pasta.  
  
-   **Gerenciador de conexões de Arquivo Simples:** você modificará o gerenciador de conexões criado na Lição 1 usando uma variável definida pelo usuário para popular a propriedade **ConnectionString** do gerenciador de conexões.  
  
Os procedimentos nessa tarefa mostram como você pode criar e modificar o contêiner Loop Foreach para usar uma variável definida pelo usuário e adicionar a tarefa de fluxo de dados ao loop. Você aprenderá como modificar o gerenciador de conexões de Arquivo Simples para usar uma variável definida pelo usuário na próxima tarefa.  
  
Após essas modificações no pacote, quando ele for executado, o contêiner Loop Foreach iterará através dessa coleção de arquivos na pasta Dados de Exemplo. Sempre que um arquivo é encontrado e corresponde ao critério, o contêiner Loop Foreach populará a variável definida pelo usuário com o nome do arquivo, mapeará a variável definida pelo usuário para a propriedade **ConnectionString** do gerenciador de conexões de Arquivo Simples dos Dados de Moeda de Exemplo e executará o fluxo de dados nesse arquivo. Portanto, em cada iteração do Loop Foreach a tarefa de Fluxo de Dados consumirá um arquivo simples diferente.  
  
> [!NOTE]  
> Como o [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa o fluxo de controle do fluxo de dados, qualquer loop que você adicionar ao fluxo de controle não exigirá modificações no fluxo de dados. Portanto, o fluxo de dados que você criou na Lição 1 não tem que ser alterado.  
  
### Para adicionar um contêiner Loop Foreach   
  
1.  Em **SQL Server Data Tools**, clique na guia **Fluxo de Controle**.  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Contêineres** e arraste um **Contêiner Loop Foreach** até a superfície de design da guia **Fluxo de Controle**.  
  
3.  Clique com o botão direito do mouse no **Contêiner Loop Foreach** recém-adicionado e selecione **Editar**.  
  
4.  Na caixa de diálogo **Editor de Loop Foreach**, na página **Geral**, em **Nome**, insira **Arquivo Foreach na Pasta**. Clique em **OK**.  
  
5.  Clique com o botão direito do mouse no contêiner Loop Foreach, clique em **Propriedades** e, na janela Propriedades, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)**.  
  
### Para configurar o enumerador para o contêiner Loop Foreach  
  
1.  Clique duas vezes em Arquivo Foreach na Pasta para abrir novamente o **Editor de Loop Foreach**.  
  
2.  Clique em **Coleção**.  
  
3.  Na página **Coleção**, selecione **Enumerador de Arquivo Foreach**.  
  
4.  No grupo **Configuração do enumerador**, clique em **Procurar**.  
  
5.  Na caixa de diálogo **Procurar pasta**, localize a pasta no computador que contém os arquivos Currency_*.txt.  
  
    Estes dados de exemplo estão incluídos com os pacotes de lição do [!INCLUDE[ssIS](../includes/ssis-md.md)]. Para baixar os dados de exemplo e os pacotes de lição, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo HYPERLINK "http://msftisprodsamples.codeplex.com/downloads/get/578097" SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
6.  Na caixa **Arquivos**, digite **Currency_\*.txt**.  
  
### Para mapear o enumerador para uma variável definida pelo usuário  
  
1.  Clique em **Mapeamentos de Variáveis**.  
  
2.  Na página **Mapeamentos de Variáveis**, na coluna **Variável**, clique na célula vazia e selecione **\<Nova Variável…>**.  
  
3.  Na caixa de diálogo **Adicionar Variável**, em **Nome**, digite **varFileName**.  
  
    > [!IMPORTANT]  
    > Nomes de variáveis fazem diferenciação de maiúsculas e minúsculas.  
  
4.  Clique em **OK**.  
  
5.  Clique em **OK** novamente para sair da caixa de diálogo **Editor de Loop Foreach**.  
  
### Para adicionar a tarefa de fluxo de dados ao loop  
  
-   Arraste a tarefa de fluxo de dados **Extrair Dados de Moeda de Exemplo** até o contêiner Loop Foreach, agora renomeado **Arquivo Foreach na Pasta**.  
  
## Próxima tarefa da lição  
[Etapa 3: Modificando o Gerenciador de Conexões de Arquivo Simples](../integration-services/step-3-modifying-the-flat-file-connection-manager.md)  
  
## Consulte também  
[Configurar um contêiner Loop Foreach](../Topic/Configure%20a%20Foreach%20Loop%20Container.md)  
[Usar variáveis em pacotes](../Topic/Use%20Variables%20in%20Packages.md)  
  
  
  
