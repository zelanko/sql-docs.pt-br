---
title: Criar o catálogo do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8db507966f9b3323e415ca7f2abfe4a12601c1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798023"
---
# <a name="create-the-ssis-catalog"></a>Criar o catálogo do SSIS
  Depois de criar e testar pacotes no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], você pode implantar os projetos que contêm os pacotes em um servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para poder implantar os projetos no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], o servidor deve conter o catálogo do `SSISDB`. O programa de instalação do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] não cria o catálogo automaticamente; você precisará criar o catálogo manualmente por meio das instruções a seguir.  
  
 Você pode criar o catálogo do SSISDB no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Você também pode criar o catálogo programaticamente usando o Windows PowerShell.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>Para criar o catálogo SSISDB no SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Conecte-se ao Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
3.  No Pesquisador de Objetos, expanda o nó de servidor, clique com o botão direito do mouse no nó **Catálogos do Integration Services** e clique em **Criar Catálogo**.  
  
4.  Clique em **Habilitar Integração CLR**.  
  
     Esse catálogo usa procedimentos armazenados CLR.  
  
5.  Clique em **Habilitar a execução automática de procedimento armazenado do Integration Services na inicialização do SQL Server** para habilitar o procedimento armazenado [catalog.startup](/sql/integration-services/system-stored-procedures/catalog-startup) a ser executado toda vez que a instância do servidor [!INCLUDE[ssIS](../includes/ssis-md.md)] for reiniciada.  
  
     O procedimento armazenado executa a manutenção do estado das operações para o catálogo SSISDB. Ele corrigirá o status de todos os pacotes que estavam sendo executados se e quando a instância do servidor [!INCLUDE[ssIS](../includes/ssis-md.md)] ficar inoperante.  
  
6.  Insira uma senha e clique em **OK**.  
  
     A senha protege a chave mestra do banco de dados que é usada para criptografar os dados do catálogo. Salve a senha em um local seguro. É recomendado que você também faça backup da chave mestra do banco de dados. Para obter mais informações, consulte [Back Up a Database Master Key](../relational-databases/security/encryption/back-up-a-database-master-key.md).  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>Para criar o catálogo do SSISDB programaticamente  
  
1.  Execute o seguinte script do PowerShell:  
  
    ```powershell
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
  
     Para obter mais exemplos de como usar o Windows PowerShell e o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices>, confira a entrada de blog [SSIS e o PowerShell no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539) em blogs.msdn.com. Para obter uma visão geral do namespace e dos exemplos de códigos, consulte a entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](https://go.microsoft.com/fwlink/?LinkId=254267)em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Catálogo do SSIS](catalog/ssis-catalog.md)   
 [Fazer backup, restaurar e mover o catálogo do SSIS](../../2014/integration-services/backup-restore-and-move-the-ssis-catalog.md)  
