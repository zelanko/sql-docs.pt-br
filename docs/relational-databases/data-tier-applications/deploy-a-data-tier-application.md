---
title: Implantar um aplicativo da camada de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
ms.openlocfilehash: db961211295a83b61478f0849feb1cd6b3fa6c7c
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907883"
---
# <a name="deploy-a-data-tier-application"></a>Implantar um aplicativo da camada de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Implante um DAC (aplicativo da camada de dados) de um pacote de DAC em uma instância existente do mecanismo de banco de dados ou do Banco de dados SQL do Azure usando um assistente ou um script do PowerShell. 
  
 O processo de implantação registra uma instância do DAC armazenando a definição do DAC no banco de dados do sistema **msdb** (**master** em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]); cria um banco de dados, em seguida o preenche com todos os objetos de banco de dados definidos no DAC.  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>Implantar o mesmo pacote de DAC várias vezes 
 É possível implantar o mesmo pacote de DAC em uma única instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] várias vezes, porém é necessário executar as implantações uma de cada vez. O nome de instância do DAC especificado para cada implantação deve ser exclusivo dentro da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Se você implantar um DAC em uma instância do Mecanismo de Banco de Dados, o DAC implantado será incorporado no **Utilitário do SQL Server** na próxima vez que o conjunto de coleta do utilitário for enviado da instância para o ponto de controle de utilitário. O DAC estará presente no nó **Aplicativos da Camada de Dados Implantados** do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Aplicativos da Camada de Dados Implantados** details page.  
  
###  <a name="database-options-and-settings"></a>Opções e configurações do banco de dados  
 Por padrão, o banco de dados criado durante a implantação terá todas as configurações padrão da instrução CREATE DATABASE, exceto:  
  
-   A ordenação de banco de dados e o nível de compatibilidade são definidos para os valores definidos no pacote de DAC. Um pacote DAC criado a partir de um projeto de banco de dados no SQL Server Developer Tools usa os valores definidos no projeto de banco de dados. Um pacote extraído de um banco de dados existente usa os valores do banco de dados original.  
  
-   É possível ajustar algumas das configurações de banco de dados, como nome de banco de dados e caminhos de arquivo, na página **Atualizar Configuração** . Não é possível definir os caminhos de arquivo durante a implantação no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Algumas opções de banco de dados, como TRUSTWORTHY, DB_CHAINING e HONOR_BROKER_PRIORITY, não podem ser ajustadas como parte do processo de implantação. Propriedades físicas, como o número de grupos de arquivos ou os números e os tamanhos de arquivos, não podem ser alteradas como parte do processo de implantação. Após a conclusão da implantação, você pode usar a instrução ALTER DATABASE, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar o banco de dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Um DAC pode ser implantado no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] executando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior. Se você criar um DAC usando uma versão posterior, o DAC poderá conter objetos sem suporte do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Você não pode implantar esses DACs nas instâncias do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
    
## <a name="security-and-permissions"></a>Segurança e permissões
Os logons de autenticação são armazenados em um pacote de DAC sem senha. Quando o pacote é implantado ou atualizado, o logon é criado como um logon desabilitado com uma senha gerada. Para habilitar os logons, conecte usando um logon com a permissão ALTER ANY LOGIN e use ALTER LOGIN para habilitar o logon e atribuir uma nova senha que possa ser comunicada ao usuário. Isso não é necessário para logons de Autenticação do Windows, porque suas senhas não são gerenciadas pelo SQL Server.  
  
 Um DAC só pode ser implantado pelos membros das funções de servidor fixas **sysadmin** ou **serveradmin** ou por logons na função de servidor fixa **dbcreator** com as permissões ALTER ANY LOGIN. A conta interna de administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada **sa** também pode implantar um DAC. 

A implantação de um DAC com logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige associação nas funções loginmanager ou serveradmin. A implantação de um DAC sem logons no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] exige a associação nas funções dbmanager ou serveradmin.  
  
## <a name="deploy-a-dac-using-the-wizard"></a>Implantar um DAC usando o assistente  
  
1.  No **Pesquisador de Objetos**, expanda o nó da instância na qual você deseja implantar o DAC.  
  
2.  Clique com o botão direito do mouse no nó **Bancos de Dados** e selecione **Implantar Aplicativo da Camada de Dados...**  
  
3.  Conclua as caixas de diálogo do assistente e clique em Concluir.

Mais informações sobre algumas das páginas de assistente abaixo: 
     
### <a name="select-dac-package-page"></a>Selecione a página Pacote de DAC  
 Especifique o pacote de DAC que contém o aplicativo da camada de dados a ser implantado. A página faz a transição por três estados.  
    
### <a name="select-the-dac-package"></a>Selecionar o pacote de DAC  
 Escolha o pacote de DAC a ser implantado. O pacote de DAC deve ser um arquivo de pacote de DAC válido e deve ter uma extensão .dacpac.  
  
 **Pacote de DAC** – Especifique o caminho e o nome de arquivo do pacote de DAC que contém o aplicativo da camada de dados a ser implantado. Você pode selecionar o botão **Procurar** no lado direito da caixa para procurar o local do pacote de DAC.  
  
 **Nome do Aplicativo** – Uma caixa somente leitura que exibe o nome do DAC atribuído quando o DAC foi criado ou extraído de um banco de dados.  
  
 **Versão** – Uma caixa somente leitura que exibe a versão atribuída quando o DAC foi criado ou extraído de um banco de dados.  
  
 **Descrição** – Uma caixa somente leitura que exibe a descrição escrita quando o DAC foi criado ou extraído de um banco de dados.  
  
### <a name="validating-the-dac-package"></a>Validando o pacote de DAC  
 Exibe uma barra de progresso enquanto o assistente confirma se o arquivo selecionado é um pacote de DAC válido. Se o pacote de DAC for validado, o assistente prosseguirá para a versão final da página **Selecionar Pacote** , em que é possível examinar os resultados da validação. Se o arquivo não for um pacote de DAC válido, o assistente permanecerá em **Selecionar Pacote de DAC**. Selecione outro pacote de DAC válido ou cancele o assistente e gere um novo pacote de DAC.  
  
  ### <a name="review-policy-page"></a>Página Analisar Política  
 Examine os resultados da avaliação da política de seleção de servidor de DAC (se usada). A política de seleção de servidor de DAC é opcional e atribuída ao DAC quando ele é criado no Visual Studio. A política usa as facetas de política de seleção de servidor para especificar as condições que uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve atender para hospedar o DAC.  
  
 **Resultados da avaliação das condições da política** – Mostra se as condições da política de implantação do DAC foram bem-sucedidas. Os resultados da avaliação de cada condição são relatados em uma linha separada.  
  
 As políticas de seleção de servidor a seguir sempre retornam false ao implantar um DAC para [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: versão do sistema operacional, idioma, pipes nomeados habilitados, plataforma, tcp habilitado.  
  
 **Ignorar violações de política** – Use esta caixa de seleção para continuar a implantação se houver falha em uma ou mais condições de política. Somente selecione essa opção se você tiver certeza de que todas as condições que falharam não impedirão o funcionamento bem-sucedido do DAC.  
   
### <a name="update-configuration-page"></a>Página Atualizar Configuração  
 Especifique os nomes da instância do DAC implantada e do banco de dados criado pela implantação e para definir opções de banco de dados.  
  
 **Nome do Banco de Dados:** – Especifique o nome do banco de dados a ser criado pela implantação. O padrão é o nome do banco de dados de origem a partir do qual o DAC foi extraído. O nome deve ser exclusivo dentro da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e está em conformidade com as regras para identificadores do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Se você alterar o nome do banco de dados, os nomes do arquivo de dados e dos arquivos de log serão alterados para corresponder ao novo valor.  
  
 O nome do banco de dados também é usado como o nome da instância do DAC. O nome da instância é exibido no nó do DAC no nó **Aplicativos da Camada de Dados** no **Pesquisador de Objetos**ou no nó **Aplicativos da Camada de Dados Implantados** no **Gerenciador do Utilitário**.  
  
 As opções a seguir não se aplicam ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]e não são exibidas durante a implantação no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **Usar o local de banco de dados padrão** – Selecione essa opção para criar os arquivos de dados e de log de banco de dados no local padrão da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Os nomes de arquivo serão criados com o uso do nome do banco de dados.  
  
 **Especificar arquivos de banco de dados** – Selecione esta opção para especificar u local ou nome diferente para os arquivos de dados e log.  
  
 **Caminho e nome do arquivo de dados: –** Especifique o caminho completo e o nome de arquivo do arquivo de dados. A caixa é populada com o caminho e o nome de arquivo padrão. Edite a cadeia de caracteres na caixa para alterar o padrão ou use o botão Procurar para navegar para a pasta em que o arquivo de dados será colocado.  
  
 **Caminho e nome do arquivo de log:** – Especifique o caminho completo e o nome de arquivo para o arquivo de log. A caixa é populada com o caminho e o nome de arquivo padrão. Edite a cadeia de caracteres na caixa para alterar o padrão ou use o botão **Procurar** para navegar para a pasta em que o arquivo de log será colocado.  
  
###  <a name="Summary"></a> Página de Resumo  
 Use esta página para examinar as ações do assistente ao implantar o DAC.  
  
 **As configurações a seguir serão usadas para implantar o DAC.** - Examine as informações exibidas para assegurar que as ações executadas estarão corretas. A janela exibe o pacote de DAC selecionado e o nome selecionado para a instância de DAC escolhida. A janela também exibe as configurações que serão usadas durante a criação do banco de dados associado ao DAC.  
   
### <a name="deploy-page"></a>Página Implantar  
 Esta página relata o êxito ou falha da operação de implantação.  
  
 **Implantando o DAC** – Relata o êxito ou falha de cada ação realizada para implantar o DAC. Analise as informações para determinar o êxito ou falha de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Selecione o link para exibir um relatório do erro para aquela ação.  
  
 **Salvar Relatório** – Selecione este botão para salvar o relatório de implantação em um arquivo HTML. O arquivo relata o status de cada ação, inclusive todos os erros gerados por qualquer uma das ações. A pasta padrão é SQL Server Management Studio\pacotes de DAC na pasta Documentos da conta do Windows.  
  
  
##  <a name="using-powershell"></a>Usando o PowerShell  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância na qual o DAC é implantado.  
  
2.  Abra um objeto **ServerConnection** e conecte-se à mesma instância.  
  
3.  Use **System.IO.File** para carregar o arquivo de pacote de DAC.  
  
4.  Use **add_DacActionStarted** e **add_DacActionFinished** para assinar eventos de implantação do DAC.  
  
5.  Defina o **DatabaseDeploymentProperties**.  
  
6.  Use o método **DacStore.Install** para implantar o DAC.  
  
7.  Feche o fluxo de arquivos usado para ler o arquivo de pacote de DAC.  

O exemplo a seguir implanta um DAC nomeado MyApplication em uma instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)], usando uma definição de DAC de um pacote de MyApplication.dacpac.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverConnection,$dacName)  
$dacStore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>Mais informações 
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Extrair um DAC de um banco de dados](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [Identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md)  
  
  
