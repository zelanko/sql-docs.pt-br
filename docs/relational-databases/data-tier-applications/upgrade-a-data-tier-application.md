---
title: Atualizar um aplicativo da camada de dados | Microsoft Docs
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
- sql13.swb.upgradedacwizard.summary.f1
- sql13.swb.upgradedacwizard.reviewplan.f1
- sql13.swb.upgradedacwizard.upgradedac.f1
- sql13.swb.upgradedacwizard.selectpackage.f1
- sql13.swb.upgradedacwizard.reviewpolicy.f1
- sql13.swb.upgradedacwizard.selectoptions.f1
- sql13.swb.upgradedacwizard.checkdrift.f1
- sql13.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: cf2d74e423ab96af582d5f420065f9756e671ec2
ms.openlocfilehash: 2a55f2852f3146cd20ace9448040c1f96d328f07
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="upgrade-a-data-tier-application"></a>Atualizar um aplicativo da camada de dados
  Use o Assistente para Atualizar Aplicativo da Camada de Dados ou um script do Windows PowerShell para alterar o esquema e as propriedades de um DAC (aplicativo da camada de dados) implantado no momento para coincidir com o esquema e as propriedades definidos em uma nova versão do DAC.  
  
-   **Antes de começar:**  [Escolhendo Opções de Atualização de DAC](#ChoseDACUpgOptions), [Limitações e Restrições](#LimitationsRestrictions), [Pré-requisitos](#Prerequisites), [Segurança](#Security), [Permissões](#Permissions)  
  
-   **Para atualizar um DAC, usando:**  [O Assistente para Atualizar o Aplicativo da Camada de Dados](#UsingDACUpgradeWizard), [PowerShell](#UpgradeDACPowerShell)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Uma atualização de DAC é um processo no local que altera o esquema do banco de dados existente para corresponder ao esquema definido em uma nova versão do DAC. A nova versão do DAC é fornecida em um arquivo de pacote DAC. Para obter mais informações sobre como criar um pacote de DAC, veja [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md).  
  
###  <a name="ChoseDACUpgOptions"></a> Escolhendo Opções de Atualização de DAC  
 Há quatro opções de atualização para uma atualização no local:  
  
-   **Ignorar Perda de Dados** – Se **True**, a atualização continuará mesmo que algumas das operações resultem na perda de dados. Se **False**, estas operações finalizarão a atualização. Por exemplo, se uma tabela no banco de dados atual não estiver presente no esquema do novo DAC, a tabela será removida se **True** for especificado. A configuração padrão é **True**.  
  
-   **Bloquear Alterações** - Se **True**, a atualização será finalizada se o esquema de banco de dados for diferente daquele definido no DAC anterior. Se **False**, a atualização continuará mesmo que sejam detectadas alterações. A configuração padrão é **False**.  
  
-   **Reversão em Falha** - Se **True**, a atualização será incluída em uma transação. Se forem encontrados erros, haverá uma tentativa de reversão. Se **False**, todas as alterações serão confirmadas à medida que ocorrerem. Se houver erros, talvez você precise restaurar um backup anterior do banco de dados. A configuração padrão é **False**.  
  
-   **Ignorar a Validação da Política** - Se **True**, a política de seleção de servidor de DAC não será avaliada. Se **False**, a política será avaliada e a atualização finalizará se houver um erro de validação. A configuração padrão é **False**.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
 Só podem ser executados uprades de DAC em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ou [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) ou posterior.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Convém fazer um backup completo do banco de dados antes de iniciar a atualização. Se uma atualização encontrar um erro e não puder reverter todas as suas alterações, talvez seja preciso restaurar o backup.  
  
 Antes de iniciar a atualização, há várias ações a serem adotadas para validar o pacote de DAC e as ações de atualização. Para obter mais informações sobre como executar essas verificações, consulte [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md).  
  
-   É recomendável não atualizar usando um pacote de DAC de origens desconhecidas ou não confiáveis. Esses pacotes podem conter código mal-intencionado que possivelmente executarão códigos Transact-SQL inesperados ou provocarão erros ao modificar o esquema. Antes de usar um pacote de uma origem desconhecida ou não confiável, desempacote o DAC e examine o código, como procedimentos armazenados ou outro código definido pelo usuário.  
  
-   Se ocorreram alterações no banco de dados atual após a implantação da última versão do DAC, algumas dessas alterações talvez impeçam a conclusão bem-sucedida da atualização, ou talvez elas sejam removidas pela atualização. Você deve primeiro gerar e examinar um relatório de revisão que inclua as alterações feitas no banco de dados.  
  
-   É aconselhável gerar uma lista das alterações a serem feitas pela atualização no esquema, além de examinar essa lista para verificar se há problemas.  
  
 O nome do aplicativo no pacote de DAC deve corresponder ao nome do aplicativo do DAC implantado no momento. Por exemplo, se o DAC atual tiver um nome de aplicativo **GeneralLedger**, somente será possível atualizar usando um pacote de DAC que também tenha um nome de aplicativo **GeneralLedger**.  
  
 Verifique se há bastante espaço de log de transação disponível para registrar todas das modificações.  
  
###  <a name="Security"></a> Segurança  
 Para melhorar a segurança, os logons de autenticação do SQL Server são armazenados em um pacote do DAC sem senha. Quando o pacote é implantado ou atualizado, o logon é criado como um logon desabilitado com uma senha gerada. Para habilitar os logons, faça logon usando um logon que tenha a permissão de ALTER ANY LOGIN e use ALTER LOGIN para habilitar o logon e atribuir uma nova senha que possa ser comunicada ao usuário. Isso não é necessário para logons de Autenticação do Windows porque suas senhas não são gerenciadas pelo SQL Server.  
  
####  <a name="Permissions"></a> Permissões  
 Um DAC pode ser atualizado somente pelos membros das funções de servidor fixas **sysadmin** ou **serveradmin** ou por logons que estejam na função de servidor fixa **dbcreator** e tenham permissões ALTER ANY LOGIN. O logon deve ser o proprietário do banco de dados existente. A conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada **sa** também pode atualizar um DAC.  
  
##  <a name="UsingDACUpgradeWizard"></a> Usando o Assistente para Atualizar Aplicativo da Camada de Dados  
 **Para atualizar um DAC usando um assistente**  
  
1.  No **Pesquisador de Objetos**, expanda o nó da instância que contém o DAC a ser atualizado.  
  
2.  Expanda os nós **Gerenciamento** e **Aplicativos da Camada de Dados** .  
  
3.  Clique com o botão direito do mouse no nó do DAC a ser atualizado e selecione **Atualizar Aplicativo da Camada de Dados…**  
  
4.  Conclua as etapas das caixas de diálogo do assistente:  
  
    1.  [Página de Introdução](#Introduction)  
  
    2.  [Página Selecionar Pacote](#Select_dac_package)  
  
    3.  [Página Analisar Política](#Review_policy)  
  
    4.  [Página Detectar Alterações](#Detect_change)  
  
    5.  [Analisar um plano de atualização](#ReviewUpgPlan)  
  
    6.  [Página de Resumo](#Summary)  
  
    7.  [Página Atualizar DAC](#Upgrade)  
  
##  <a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas para atualizar um aplicativo da camada de dados.  
  
 **Não mostrar esta página novamente.** - Clique na caixa de seleção para interromper a exibição da página no futuro.  
  
 **Avançar >** – Segue para a página **Selecionar Pacote**.  
  
 **Cancelar** – Encerra o assistente sem atualizar o DAC.  
  
##  <a name="Select_dac_package"></a> Página Selecionar Pacote  
 Use esta página para especificar o pacote de DAC que contém a nova versão do aplicativo da camada de dados. A página faz a transição por dois estados.  
  
### <a name="select-the-dac-package"></a>Selecionar o pacote de DAC  
 Use o estado inicial da página para escolher o pacote de DAC a ser implantado. O pacote de DAC deve ser um arquivo de pacote de DAC válido e deve ter uma extensão .dacpac. O nome do aplicativo de DAC no pacote de DAC deve ser igual ao nome do aplicativo do DAC atual.  
  
 **Pacote de DAC** – Especifique o caminho e o nome de arquivo do pacote de DAC que contém a nova versão do aplicativo da camada de dados. Você pode selecionar o botão **Procurar** no lado direito da caixa para procurar o local do pacote de DAC.  
  
 **Nome do Aplicativo** – Uma caixa somente leitura que exibe o nome do aplicativo de DAC atribuído quando o DAC foi criado ou extraído de um banco de dados.  
  
 **Versão** – Uma caixa somente leitura que exibe a versão atribuída quando o DAC foi criado ou extraído de um banco de dados.  
  
 **Descrição** – Uma caixa somente leitura que exibe a descrição escrita quando o DAC foi criado ou extraído de um banco de dados.  
  
 **< Anterior** – Retorna à página **Introdução**.  
  
 **Avançar >** – Exibe uma barra de progresso enquanto o assistente confirma se o arquivo selecionado é um pacote de DAC válido.  
  
 **Cancelar** – Encerra o assistente sem atualizar o DAC.  
  
### <a name="validating-the-dac-package"></a>Validando o pacote de DAC  
 Exibe uma barra de progresso enquanto o assistente confirma se o arquivo selecionado é um pacote de DAC válido. Se o pacote de DAC for validado, o assistente seguirá para a página **Examinar Política** . Se o arquivo não for um pacote de DAC válido, o assistente permanecerá na página **Selecionar Pacote de DAC** . Selecione outro pacote de DAC válido ou cancele o assistente e gere um novo pacote de DAC.  
  
 **Validando o conteúdo do DAC** – A barra de progresso que relata o status atual do processo de validação.  
  
 **< Anterior** – Retorna ao estado inicial da página **Selecionar Pacote**.  
  
 **Avançar >** – Segue para a versão final da página **Selecionar Pacote**.  
  
 **Cancelar** – Encerra o assistente sem implantar o DAC.  
  
##  <a name="Review_policy"></a> Página Analisar Política  
 Use esta página para examinar os resultados da avaliação da política de seleção de servidor de DAC, se o DAC tiver uma política. A política de seleção de servidor de DAC é opcional e atribuída a um DAC criado no Microsoft Visual Studio. A política usa as facetas de política de seleção de servidor para especificar as condições que uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve atender para hospedar o DAC.  
  
 **Resultados da avaliação das condições da política** – Um relatório somente leitura que mostra se as avaliações das condições na política de seleção de servidor de DAC foram bem-sucedidas. Os resultados da avaliação de cada condição são relatados em uma linha separada.  
  
 **Ignorar violações de política** – Use esta caixa de seleção para continuar com a atualização se uma ou mais condições de política falharem. Somente selecione essa opção se você tiver certeza de que todas as condições que falharam não impedirão o funcionamento bem-sucedido do DAC.  
  
 **< Anterior** – Retorna à página **Selecionar Pacote**.  
  
 **Avançar >** – Segue para a página **Detectar Alteração**.  
  
 **Cancelar** – Encerra o assistente sem atualizar o DAC.  
  
##  <a name="Detect_change"></a> Página Detectar Alterações  
 O uso desta página relata os resultados da verificação dos assistentes quanto às alterações feitas no banco de dados que tornam esse esquema diferente da definição de esquema armazenada nos metadados do DAC no **msdb**. Por exemplo, se as instruções CREATE, ALTER ou DROP tiverem sido usadas para adicionar, alterar ou remover objetos do banco de dados após a implantação original do DAC. Primeiro, a página exibe uma barra de progresso e depois relata os resultados da análise.  
  
 **Detectando alteração, isso pode demorar alguns minutos** – Exibe uma barra de progresso enquanto o assistente verifica as diferenças entre o esquema atual do banco de dados e os objetos na definição do DAC.  
  
 **Resultados da detecção de alterações:** – Indica se a análise foi concluída e os resultados são relatados abaixo.  
  
 **O banco de dados DatabaseName não foi alterado** – O assistente não detectou diferenças nos objetos definidos no banco de dados e em suas contrapartes na definição do DAC.  
  
 **O banco de dados DatabaseName foi alterado** – O assistente detectou alterações entre os objetos no banco de dados e em suas contrapartes na definição do DAC.  
  
 **Continuar, apesar da possível perda de alterações** – Especifique que você entende que alguns dos objetos ou dados no banco de dados atual não estarão presentes no novo banco de dados e que está disposto a continuar com a atualização. Somente selecione este botão se você tiver analisado o relatório de alterações e entender as etapas que deve executar para transferir manualmente os objetos ou os dados necessários no novo banco de dados. Se você não tiver certeza, clique no botão **Salvar Relatório** para salvar o relatório de alterações e clique em **Cancelar**. Analise o relatório, faça um planejamento de como transferir os objetos e os dados necessários após a conclusão da atualização e reinicie o assistente.  
  
 **Salvar Relatório** – Clique no botão para salvar um relatório das alterações que o assistente detectou entre os objetos no banco de dados e suas contrapartes na definição do DAC. Em seguida, você pode examinar o relatório para determinar se precisa executar ações após a conclusão da atualização para incorporar alguns ou todos os objetos listados no relatório para o novo banco de dados.  
  
 **< Anterior** – Retorna à página **Selecionar Pacote de DAC**.  
  
 **Avançar >** – Segue para a página **Opções**.  
  
 **Cancelar** – Encerra o assistente sem implantar o DAC.  
  
## <a name="options-page"></a>Página Opções  
 Use esta página para selecionar a reversão em opção de falha para a atualização.  
  
 **Reversão em falha** – Selecione esta opção para incluir a atualização em uma transação que o assistente pode tentar reverter em caso de erros. Para obter mais informações sobre a opção, consulte [Escolhendo Opções de Atualização de DAC](#ChoseDACUpgOptions).  
  
 **Restaurar Padrões** – Retorna a opção à configuração padrão de false.  
  
 **< Anterior** – Retorna à página **Detectar Alteração**.  
  
 **Avançar >** – Segue para a página **Examinar o Plano de Atualização**.  
  
 **Cancelar** – Encerra o assistente sem implantar o DAC.  
  
##  <a name="ReviewUpgPlan"></a> Página Analisar um plano de atualização  
 Use esta página para examinar as ações que serão tomadas pelo processo de atualização. Só prossiga quando estiver certo de que a atualização não criará problemas.  
  
 **As ações a seguir serão usadas para atualizar o DAC.** - Examine as informações exibidas para assegurar que as ações executadas estarão corretas. A coluna **Ação** exibe as ações, tais como instruções Transact-SQL, que serão executadas para realizar a atualização. A coluna **Perda de Dados** conterá um aviso se a ação associada puder excluir dados.  
  
 **Atualizar** - atualiza a lista de ações.  
  
 **Salvar Relatório de Ação** - salva o conteúdo da janela de ação em um arquivo HTML.  
  
 **Continuar, apesar da possível perda de alterações** – Especifique que você entende que alguns dos objetos ou dados no banco de dados atual não estarão presentes no novo banco de dados e que está disposto a continuar com a atualização. Somente selecione este botão se você tiver analisado o relatório de alterações e entender as etapas que deve executar para transferir manualmente os objetos ou os dados necessários no novo banco de dados. Se você não tiver certeza, clique no botão **Salvar Relatório de Ação** para salvar o relatório de alterações e no botão **Salvar Scripts** para salvar o script Transact-SQL. Depois, clique em **Cancelar**. Analise o relatório e o script. Em seguida, planeje como transferir os objetos e os dados necessários após a conclusão da atualização. Reinicie o assistente.  
  
 **Salvar Scripts** – salva as instruções Transact-SQL que serão usadas para executar a atualização em um arquivo de texto.  
  
 **Restaurar Padrões** – Retorna a opção à configuração padrão de false.  
  
 **< Anterior** – Retorna à página **Detectar Alteração**.  
  
 **Avançar >**: continua para a página **Resumo**.  
  
 **Cancelar** – Encerra o assistente sem implantar o DAC.  
  
##  <a name="Summary"></a> Página de Resumo  
 Use esta página para fazer uma análise final das ações do assistente ao atualizar o DAC.  
  
 **As configurações a seguir serão usadas para atualizar o DAC.** - Examine as informações exibidas para assegurar que as ações executadas estarão corretas. A janela exibe o DAC selecionado para atualização e o pacote de DAC que contém a nova versão do DAC. A janela também exibe se a versão atual do banco de dados é igual à definição de DAC atual, ou se o banco de dados foi alterado.  
  
 **< Anterior** – Retorna à página **Examinar o Plano de Atualização**.  
  
 **Avançar >** – Implanta o DAC e exibe os resultados na página **Atualizar DAC**.  
  
 **Cancelar** – Encerra o assistente sem implantar o DAC.  
  
##  <a name="Upgrade"></a> Página Atualizar DAC  
 Esta página relata o êxito ou falha da operação de atualização.  
  
 **Atualizando o DAC** – Relata o êxito ou falha de cada ação realizada para atualizar o DAC. Analise as informações para determinar o êxito ou falha de cada ação. Todas as ações que encontrarem um erro terão um link na coluna **Resultado** . Selecione o link para exibir um relatório do erro para aquela ação.  
  
 **Salvar Relatório** – Selecione esse botão para salvar o relatório de atualização em um arquivo HTML. O arquivo relata o status de cada ação, inclusive todos os erros gerados por qualquer uma das ações. A pasta padrão é uma pasta SQL Server Gerenciamento Studio\Pacotes de DAC na pasta Documentos da conta do Windows.  
  
 **Concluir** – Encerra o assistente.  
  
##  <a name="UpgradeDACPowerShell"></a> Usando o PowerShell  
 **Para atualizar um DAC que usa o método IncrementalUpgrade() em um script do PowerShell**  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância que contém o DAC a ser atualizado.  
  
2.  Abra um objeto **ServerConnection** e conecte-se à mesma instância.  
  
3.  Use **System.IO.File** para carregar o arquivo de pacote de DAC.  
  
4.  Use **add_DacActionStarted** e **add_DacActionFinished** para assinar eventos de atualização do DAC.  
  
5.  Defina o **DacUpgradeOptions**.  
  
6.  Use o método **IncrementalUpgrade** para atualizar o DAC.  
  
7.  Feche o fluxo de arquivos usado para ler o arquivo de pacote de DAC.  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 O exemplo a seguir faz upgrade de um DAC denominado MyApplication em uma instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)], usando uma nova versão de DAC em um pacote MyApplication2017.dacpac.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication2017.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

