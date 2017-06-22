---
title: Excluir um aplicativo da camada de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deletedacwizard.deletedac.f1
- sql13.swb.deletedacwizard.summary.f1
- sql13.swb.deletedacwizard.introduction.f1
- sql13.swb.deletedacwizard.choosemethod.f1
helpviewer_keywords:
- How to [DAC], delete
- data-tier application [SQL Server], delete
- wizard [DAC], delete
- delete DAC
ms.assetid: 16fe1c18-4486-424d-81d6-d276ed97482f
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a6c69a8bbd4fa63a427658ddc7b8fdbd79b0af3b
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-data-tier-application"></a>Excluir um Aplicativo da Camada de Dados
  Você poderá excluir um aplicativo da camada de dados usando o Assistente para Excluir Aplicativo da Camada de Dados ou um script do Windows PowerShell. É possível especificar se o banco de dados associado será retido, desanexado ou removido.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To upgrade a DAC, using:**  [The Register Data-tier Application Wizard](#UsingDeleteDACWizard), [PowerShell](#DeleteDACPowerShell)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Ao excluir uma instância de DAC (aplicativo da camada de dados), você escolhe uma das três opções que especificam o que será feito com o banco de dados associado ao aplicativo da camada de dados. Todas as três opções excluem os metadados da definição do DAC. As opções diferem no que fazem com o banco de dados associado ao aplicativo da camada de dados. O assistente não exclui nenhum dos objetos do nível de instância associados ao DAC ou banco de dados, como logons.  
  
|Opção|Ações de banco de dados|  
|------------|----------------------|  
|Excluir registro|O banco de dados associado permanece intacto.|  
|Desanexar banco de dados|O banco de dados associado é desanexado. A instância do Mecanismo de Banco de Dados não pode fazer referência ao banco de dados, mas os dados e os arquivos de log estão intatos.|  
|Excluir banco de dados|O banco de dados associado é removido. Os dados e os arquivos de log são excluídos.|  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Não há nenhum mecanismo automático para restaurar os metadados da definição do DAC ou o banco de dados depois que um DAC é excluído. A maneira como a instância do DAC pode ser recriada manualmente depende da opção de exclusão.  
  
|Opção|Como recriar a instância do DAC|  
|------------|-------------------------------------|  
|Excluir registro|Registrar um DAC do banco de dados deixado no lugar.|  
|Desanexar banco de dados|Reanexe o banco de dados usando **sp_attachdb** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e registre uma nova instância de DAC do banco de dados.|  
|Excluir banco de dados|Restaure o banco de dados de um backup completo feito antes do DAC ser excluído e registre uma nova instância do DAC no banco de dados.|  
  
> [!WARNING]  
>  A recompilação de uma instância de DAC através do registro de um DAC em um banco de dados restaurado ou reanexado não recriará algumas partes do DAC original, como a política de seleção de servidor.  
  
###  <a name="Permissions"></a> Permissões  
 Um DAC pode ser excluído somente pelos membros das funções de servidor fixas **sysadmin** ou **serveradmin** , ou pelo proprietário do banco de dados. A conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada **sa** também pode iniciar o assistente.  
  
##  <a name="UsingDeleteDACWizard"></a> Usando o Assistente para Excluir Aplicativo da Camada de Dados  
 **Para excluir um DAC usando um assistente**  
  
1.  No **Pesquisador de Objetos**, expanda o nó da instância que contém o DAC a ser excluído.  
  
2.  Expanda o nó **Gerenciamento** .  
  
3.  Expanda o nó **Aplicativos da Camada de Dados** .  
  
4.  Clique com o botão direito do mouse no DAC a ser excluído e selecione **Excluir Aplicativo da Camada de Dados...**  
  
5.  Conclua as etapas das caixas de diálogo do assistente:  
  
    1.  [Introdução](#Introduction)  
  
    2.  [Escolher método](#Choose_method)  
  
    3.  [Resumo](#Summary)  
  
    4.  [Excluir Aplicativo da Camada de Dados](#Delete_datatier_application)  
  
##  <a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas para excluir um aplicativo da camada de dados.  
  
 **Não mostrar esta página novamente.** - Clique na caixa de seleção para interromper a exibição da página no futuro.  
  
 **Avançar >**: continua para a página **Escolher Método**.  
  
 **Cancelar** : finaliza o assistente sem excluir um aplicativo da camada de dados ou banco de dados.  
  
 [Usando o Assistente para Excluir Aplicativo da Camada de Dados](#UsingDeleteDACWizard)  
  
##  <a name="Choose_method"></a> Página Escolher Método  
 Use esta página para especificar a opção que tratará o banco de dados associado ao DAC que será excluído.  
  
 **Excluir registro** : remove os metadados que definem o aplicativo da camada de dados, mas deixa o banco de dados associado intacto.  
  
 **Desanexar banco de dados** : remove os metadados que definem o aplicativo da camada de dados e desanexa o banco de dados associado.  
  
 O banco de dados não pode mais ser referenciado por aquela instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], mas os dados e os arquivos de log permanecem intactos.  
  
 **Excluir banco de dados** : remove os metadados que definem o DAC e descarta o banco de dados associado.  
  
 Os dados e os arquivos de log do banco de dados são excluídos permanentemente.  
  
 **< Anterior** – Retorna à página **Introdução**.  
  
 **Avançar >**: continua para a página **Resumo**.  
  
 **Cancelar** : finaliza o assistente sem excluir o DAC ou o banco de dados.  
  
 [Usando o Assistente para Excluir Aplicativo da Camada de Dados](#UsingDeleteDACWizard)  
  
##  <a name="Summary"></a> Página de Resumo  
 Use esta página para examinar as ações que o assistente tomará ao excluir a instância do DAC.  
  
 **Review your selection summary (Examinar o resumo de sua seleção)** : examine o DAC, o banco de dados e o método de exclusão exibidos na caixa. Se as informações estiverem corretas, selecione **Avançar** ou **Concluir** para excluir o DAC. Se o DAC e as informações do banco de dados não estiverem corretas, selecione **Cancelar** e selecione o DAC correto. Se o método de exclusão não estiver correto, selecione **Anterior** para retornar ou a página **Escolher Método** e selecione um método diferente.  
  
 **< Anterior**: retorna para a página **Escolher Método** para escolher um método de exclusão diferente.  
  
 **Avançar >**: exclui a instância de DAC usando o método escolhido na página anterior e continua para a página **Excluir Aplicativo da Camada de Dados**.  
  
 **Cancelar** : finaliza o assistente sem excluir a instância de DAC.  
  
 [Usando o Assistente para Excluir Aplicativo da Camada de Dados](#UsingDeleteDACWizard)  
  
##  <a name="Delete_datatier_application"></a> Página Excluir Aplicativo da Camada de Dados  
 Esta página relata o êxito ou a falha da operação de exclusão.  
  
 **Excluindo o DAC** : relata o êxito ou falha de cada ação realizada para excluir a instância de DAC. Analise as informações para determinar o êxito ou falha de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Selecione o link para exibir um relatório do erro para aquela ação.  
  
 **Salvar Relatório** : selecione esse botão para salvar o relatório de exclusão em um arquivo HTML. O arquivo relata o status de cada ação, inclusive todos os erros gerados por qualquer uma das ações. A pasta padrão é SQL Server Management Studio\DAC Packages na pasta Documents da conta do Windows.  
  
 **Concluir** : finaliza o assistente.  
  
 [Usando o Assistente para Excluir Aplicativo da Camada de Dados](#UsingDeleteDACWizard)  
  
##  <a name="DeleteDACPowerShell"></a> Excluir um DAC usando o PowerShell  
 **Para excluir um DAC usando o script do PowerShell**  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância que contém o DAC a ser excluído.  
  
2.  Abra um objeto **ServerConnection** e conecte-se à mesma instância.  
  
3.  Use **add_DacActionStarted** e **add_DacActionFinished** para assinar eventos de atualização do DAC.  
  
4.  Especifique o DAC a ser excluído.  
  
5.  Use um destes três conjuntos de códigos, dependendo da opção de exclusão apropriada:  
  
    -   Para excluir o registro do DAC, mas deixar o banco de dados intacto, use o método **Unmanage()** .  
  
    -   Para excluir o registro do DAC e desanexar o banco de dados, use o método **Uninstall()** e especifique **DetachDatabase**.  
  
    -   Para excluir o registro do DAC e remover o banco de dados, use o método **Uninstall()** e especifique **DropDatabase**.  
  
### <a name="example-deleting-the-dac-but-leaving-the-database-powershell"></a>Exemplo Excluindo o DAC mas deixando o banco de dados (PowerShell)  
 O exemplo a seguir exclui um DAC chamado MyApplication usando o método **Unmanaged()** para excluir o DAC, mas deixar o banco de dados intacto.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Only delete the DAC definition from msdb, the associated database remains active.  
$dacstore.Unmanage($dacName)  
```  
  
 [Excluir um DAC usando o PowerShell](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-detaching-the-database-powershell"></a>Exemplo Excluindo o DAC e desanexando o banco de dados (PowerShell)  
 O exemplo a seguir exclui um DAC chamado MyApplication usando o método **Uninstall()** para excluir o DAC e desanexar o banco de dados.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and detach the associated database.  
$dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DetachDatabase)  
```  
  
 [Excluir um DAC usando o PowerShell](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-dropping-the-database-powershell"></a>Exemplo Excluindo o DAC e removendo o banco de dados (PowerShell)  
 O exemplo a seguir exclui um DAC chamado MyApplication usando o método **Uninstall()** para excluir o DAC e remover o banco de dados.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and drop the associated database.  
## $dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DropDatabase)  
```  
  
 [Excluir um DAC usando o PowerShell](#DeleteDACPowerShell)  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Implantar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Registrar um banco de dados como um DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

