---
title: Validar um pacote de DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: data-tier-applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], validate
- data-tier application [SQL Server], compare
- validate DAC
- compare DACs
- data-tier application [SQL Server], view
- view DAC
ms.assetid: 726ffcc2-9221-424a-8477-99e3f85f03bd
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 909fa2d13ac8cceab6127409bfd770dd00606359
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32931202"
---
# <a name="validate-a-dac-package"></a>Validar um pacote de DAC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta é uma prática recomendada para revisar o conteúdo de um pacote de DAC antes de implantá-lo em produção e também para validar as ações de atualização antes de atualizar um DAC existente. Isso é especialmente válido durante a implantação de pacotes que não foram desenvolvidos em sua organização.  
  
1.  **Antes de começar:**  [Pré-requisitos](#Prerequisites)  
  
2.  **Para atualizar um DAC, usando:**  [Exibir o Conteúdo de um DAC](#ViewDACContents), [Exibir Alterações no Banco de Dados](#ViewDBChanges), [Exibir Ações de Atualização](#ViewUpgradeActions), [Compare DACs](#CompareDACs)  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
 Recomendamos não implantar um pacote de DAC de origens desconhecidas ou não confiáveis. Como os DACs podem conter código mal-intencionado que pode executar código [!INCLUDE[tsql](../../includes/tsql-md.md)] sem finalidade ou provocar erros modificando o esquema. Antes de usar um DAC de uma origem desconhecida ou não confiável, implante-o em uma instância de teste isolada do [!INCLUDE[ssDE](../../includes/ssde-md.md)], execute [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
##  <a name="ViewDACContents"></a> Exibir o Conteúdo de um DAC  
 Existem dois mecanismos para exibição do conteúdo de um pacote de DAC (aplicativo da camada de dados). Você pode importar o pacote de DAC para um projeto de DAC no SQL Server Developer Tools. É possível desempacotar o conteúdo do pacote em uma pasta.  
  
 **Exiba um DAC no SQL Server Developer Tools**  
  
1.  Abra o menu **Arquivo** , selecione **Novo**e, em seguida, selecione **Projeto…**.  
  
2.  Selecione o modelo de projeto **SQL Server** e especifique um **Nome**, um **Local**e um **Nome de solução**.  
  
3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó e selecione **Propriedades…**.  
  
4.  Na guia **Configurações de Projeto** , na seção **Tipos de Saída** , marque a caixa de seleção **Aplicativo da Camada de Dados (arquivo .dacpac)** e feche a caixa de diálogo de propriedades.  
  
5.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Importar Aplicativo da Camada de Dados…**.  
  
6.  Use o **Gerenciador de Soluções** para abrir todos os arquivos no DAC, como a política de seleção de servidor e os scripts de pré e pós-implantação.  
  
7.  Use a **Exibição de Esquema** para examinar todos os objetos no esquema, especialmente o código em objetos, como funções ou procedimentos armazenados.  
  
 **Exibir um DAC em uma pasta**  
  
-   Desempacote o pacote de DAC em uma pasta seguindo as instruções em [Unpack a DAC Package](../../relational-databases/data-tier-applications/unpack-a-dac-package.md).  
  
-   Exiba os conteúdo dos scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] abrindo-os no Editor de Consulta [!INCLUDE[ssDE](../../includes/ssde-md.md)] no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
-   Exiba o conteúdo dos arquivos de texto em ferramentas como o bloco de notas.  
  
##  <a name="ViewDBChanges"></a> Exibir Alterações no Banco de Dados  
 Depois que a versão atual de um DAC for implantada para produção, alterações poderão ter sido feitas diretamente no banco de dados associado que podem estar em conflito com o esquema definido em uma nova versão do DAC. Antes de atualizar para uma nova versão do DAC, verifique se foram feitas alterações no banco de dados.  
  
 **Exibir alterações do banco de dados usando um assistente**  
  
1.  Execute o assistente para **Atualizar Aplicativo da Camada de Dados** , especificando o DAC implantado no momento e o pacote de DAC que contém a nova versão do DAC.  
  
2.  Na página **Detectar Alteração** , examine o relatório das alterações que foram feitas no banco de dados.  
  
3.  Selecione **Cancelar** se não desejar continuar com a atualização.  
  
4.  Para obter mais informações sobre como usar o assistente, veja [Atualizar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md).  
  
 **Exibir alterações do banco de dados usando o PowerShell**  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância que contém o DAC a ser exibido.  
  
2.  Abra um objeto **ServerConnection** e conecte-se à mesma instância.  
  
3.  Especifique o nome de DAC em uma variável.  
  
4.  Use o método **GetDatabaseChanges()** para recuperar um objeto **ChangeResults** e redirecione o objeto para um arquivo de texto para gerar um relatório simples de objetos novos, excluídos e alterados.  
  
### <a name="view-database-changes-example-powershell"></a>Exibir exemplo de alterações do banco de dados (PowerShell)  
 **Exibir exemplo de alterações do banco de dados (PowerShell)**  
  
 O exemplo a seguir relata alterações de banco de dados realizadas em um DAC implantado denominado MyApplicaiton.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the change list and save to file.  
$dacChanges = $dacstore.GetDatabaseChanges($dacName) | Out-File -Filepath C:\DACScripts\MyApplicationChanges.txt  
```  
  
##  <a name="ViewUpgradeActions"></a> Exibir Ações de Atualização  
 Antes de usar uma nova versão de um pacote de DAC para atualizar um DAC que foi implantado de um pacote de DAC anterior, você pode gerar um relatório que contém as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a serem executadas durante a atualização e, depois, examinar as instruções.  
  
 **Relate ações de atualização usando um assistente**  
  
1.  Execute o assistente para **Atualizar Aplicativo da Camada de Dados** , especificando o DAC implantado no momento e o pacote de DAC que contém a nova versão do DAC.  
  
2.  Na página **Resumo** , examine o relatório das ações de atualização.  
  
3.  Selecione **Cancelar** se não desejar continuar com a atualização.  
  
4.  Para obter mais informações sobre como usar o assistente, veja [Atualizar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md).  
  
 **Relate ações de atualização usando o PowerShell**  
  
1.  Crie um objeto de servidor SMO e defina-o como a instância que contém o DAC implantado.  
  
2.  Abra um objeto **ServerConnection** e conecte-se à mesma instância.  
  
3.  Use **System.IO.File** para carregar o arquivo de pacote de DAC.  
  
4.  Especifique o nome de DAC em uma variável.  
  
5.  Use o método **GetIncrementalUpgradeScript()** para obter uma lista das instruções Transact-SQL que uma atualização executará e redirecione a lista para um arquivo de texto.  
  
6.  Feche o fluxo de arquivos usado para ler o arquivo de pacote de DAC.  
  
### <a name="view-upgrade-actions-example-powershell"></a>Exibir o exemplo de ações de atualização (PowerShell)  
 **Exibir o exemplo de ações de atualização (PowerShell)**  
  
 O exemplo a seguir relata as instruções Transact-SQL que seriam executadas para atualizar um DAC denominado MyApplicaiton ao esquema definido em um arquivo MyApplication2017.dacpac.  
  
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
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the upgrade script and save to file.  
$dacstore.GetIncrementalUpgradeScript($dacName, $dacType) | Out-File -Filepath C:\DACScripts\MyApplicationUpgrade.sql  
  
## Close the filestream to the new DAC package.  
$fileStream.Close()  
```  
  
##  <a name="CompareDACs"></a> Compare DACs  
 Antes de atualizar um DAC, é recomendável revisar as diferenças nos objetos em nível de banco de dados e instância entre o DAC atual e o novo. Se você não tiver uma cópia do pacote para o DAC atual, poderá extrair um pacote do banco de dados atual.  
  
 Se você importar os pacotes de DAC para projetos de DAC no SQL Server Developer Tools, poderá usar a ferramenta de comparação de esquemas para analisar as diferenças entre o dois DACs.  
  
 Outra alternativa é desempacotar os DACs em pastas separadas. Você pode usar uma ferramenta de diferenças, como o utilitário WinDiff, para analisar as diferenças.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Implantar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Atualizar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
