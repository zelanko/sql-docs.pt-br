---
title: Criar o catálogo do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8565d4957688349253b0074174dd379ba284a231
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115941"
---
# <a name="create-the-ssis-catalog"></a>Criar o catálogo do SSIS
  Depois de criar e testar pacotes no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], você pode implantar os projetos que contêm os pacotes em um servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Antes de implantar os projetos para o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] server, o servidor deve conter o `SSISDB` catálogo. O programa de instalação do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] não cria o catálogo automaticamente; você precisará criar o catálogo manualmente por meio das instruções a seguir.  
  
 Você pode criar o catálogo do SSISDB no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Você também pode criar o catálogo programaticamente usando o Windows PowerShell.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>Para criar o catálogo SSISDB no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Conecte-se ao Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
3.  No Pesquisador de Objetos, expanda o nó de servidor, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Criar Catálogo**.  
  
4.  Clique em **Habilitar Integração CLR**.  
  
     Esse catálogo usa procedimentos armazenados CLR.  
  
5.  Clique em **Habilitar a execução automática de procedimento armazenado do Integration Services na inicialização do SQL Server** para habilitar o procedimento armazenado [catalog.startup](/sql/integration-services/system-stored-procedures/catalog-startup) a ser executado toda vez que a instância do servidor [!INCLUDE[ssIS](../includes/ssis-md.md)] for reiniciada.  
  
     O procedimento armazenado executa a manutenção do estado das operações para o catálogo SSISDB. Ele corrigirá o status de todos os pacotes que estavam sendo executados se e quando a instância do servidor [!INCLUDE[ssIS](../includes/ssis-md.md)] ficar inoperante.  
  
6.  Digite uma senha e clique em **Ok**.  
  
     A senha protege a chave mestra do banco de dados que é usada para criptografar os dados do catálogo. Salve a senha em um local seguro. É recomendado que você também faça backup da chave mestra do banco de dados. Para saber mais, confira [Back Up a Database Master Key](../relational-databases/security/encryption/back-up-a-database-master-key.md)(Fazer backup de uma chave mestra de banco de dados).  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>Para criar o catálogo do SSISDB programaticamente  
  
1.  Execute o seguinte script do PowerShell:  
  
    ```  
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()  
  
    ```  
  
     Para obter mais exemplos de como usar o Windows PowerShell e o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices>, confira a entrada de blog [SSIS e o PowerShell no SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539) em blogs.msdn.com. Para obter uma visão geral do namespace e dos exemplos de códigos, consulte a entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](http://go.microsoft.com/fwlink/?LinkId=254267)em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Catálogo do SSIS](catalog/ssis-catalog.md)   
 [Fazer backup, restaurar e mover o catálogo do SSIS](../../2014/integration-services/backup-restore-and-move-the-ssis-catalog.md)  
  
  
