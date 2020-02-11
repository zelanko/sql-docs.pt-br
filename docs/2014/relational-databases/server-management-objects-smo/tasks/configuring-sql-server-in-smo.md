---
title: Configurando SQL Server em SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13fc00425a12737000a6400c5b9368288de80aa3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797236"
---
# <a name="configuring-sql-server-in-smo"></a>Configurando o SQL Server no SMO
  No SMO, o <xref:Microsoft.SqlServer.Management.Smo.Information> objeto <xref:Microsoft.SqlServer.Management.Smo.Settings> , o objeto, o <xref:Microsoft.SqlServer.Management.Smo.UserOptions> objeto e o <xref:Microsoft.SqlServer.Management.Smo.Configuration> objeto contêm configurações e informações para a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem várias propriedades que descrevem o comportamento da instância instalada. As propriedades descrevem opções de inicialização, os padrões do servidor, arquivos e diretórios, informações sobre o sistema e o processador, produtos e versões, informações sobre conexões, opções de memória, seleções de linguagem e ordenação, e o modo de autenticação.  
  
## <a name="sql-server-configuration"></a>Configuração do SQL Server  
 As propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Information> contêm informações sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], tais como processador e plataforma.  
  
 As propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.Settings> contêm informações sobre a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O diretório e o arquivo de banco de dados padrão podem ser modificados, além do Perfil de Email e da Conta de Servidor. Essas propriedades serão mantidas enquanto durar a conexão.  
  
 As propriedades do objeto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> contêm informações sobre o comportamento das conexões atuais em relação a aritmética, padrões ANSI e transações.  
  
 Também há um conjunto de opções de configuração que é representado pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Configuration>. Ele contém um conjunto de propriedades que representam as opções que podem ser modificadas pelo procedimento armazenado `sp_configure`. Opções como **aumento de prioridade**, **intervalo de recuperação** e tamanho do pacote de **rede**controlam o desempenho [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]da instância do. Muitas dessas opções podem ser alteradas de forma dinâmica, mas, em alguns casos, o valor é primeiro configurado e depois alterado quando a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é reiniciada.  
  
 Há uma propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Configuration> para cada opção de configuração. Usando o objeto <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>, você pode modificar o parâmetro de configuração global. Muitas propriedades têm valores máximo e mínimo que também são armazenados como propriedades <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>. Essas propriedades exigem o <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> método para confirmar a alteração na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Todas as opções de configuração no objeto <xref:Microsoft.SqlServer.Management.Smo.Configuration> devem ser alteradas pelo administrador do sistema.  
  
## <a name="examples"></a>Exemplos  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>Modificando as opções de configuração do SQL Server no Visual Basic  
 O exemplo de código mostra como atualizar uma opção de configuração no Visual Basic .NET. Ele também recupera e exibe informações sobre os valores máximo e mínimo da opção de configuração especificada. Finalmente, o programa informa ao usuário se a alteração foi feita dinamicamente ou se ela foi armazenada até o reinício da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure2](SMO How to#SMO_VBConfigure2)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>Modificando configurações do SQL Server no Visual Basic  
 O exemplo de código exibe informações sobre a instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do <xref:Microsoft.SqlServer.Management.Smo.Information> no <xref:Microsoft.SqlServer.Management.Smo.Settings>e do, e modifica as <xref:Microsoft.SqlServer.Management.Smo.Settings> configurações <xref:Microsoft.SqlServer.Management.Smo.UserOptions>nas propriedades do objeto e.  
  
 No exemplo, ambos os objetos <xref:Microsoft.SqlServer.Management.Smo.UserOptions> e <xref:Microsoft.SqlServer.Management.Smo.Settings> têm um método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Você pode executar os métodos <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> para eles individualmente.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure1](SMO How to#SMO_VBConfigure1)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>Modificando configurações do SQL Server no Visual C#  
 O exemplo de código exibe informações sobre a instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do <xref:Microsoft.SqlServer.Management.Smo.Information> no <xref:Microsoft.SqlServer.Management.Smo.Settings>e do, e modifica as <xref:Microsoft.SqlServer.Management.Smo.Settings> configurações <xref:Microsoft.SqlServer.Management.Smo.UserOptions>nas propriedades do objeto e.  
  
 No exemplo, ambos os objetos <xref:Microsoft.SqlServer.Management.Smo.UserOptions> e <xref:Microsoft.SqlServer.Management.Smo.Settings> têm um método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Você pode executar os métodos <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> para eles individualmente.  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```csharp
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>Modificando configurações do SQL Server no PowerShell  
 O exemplo de código exibe informações sobre a instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do <xref:Microsoft.SqlServer.Management.Smo.Information> no <xref:Microsoft.SqlServer.Management.Smo.Settings>e do, e modifica as <xref:Microsoft.SqlServer.Management.Smo.Settings> configurações <xref:Microsoft.SqlServer.Management.Smo.UserOptions>nas propriedades do objeto e.  
  
 No exemplo, ambos os objetos <xref:Microsoft.SqlServer.Management.Smo.UserOptions> e <xref:Microsoft.SqlServer.Management.Smo.Settings> têm um método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Você pode executar os métodos <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> para eles individualmente.  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>Modificando as opções de configuração do SQL Server no PowerShell  
 O exemplo de código mostra como atualizar uma opção de configuração no Visual Basic .NET. Ele também recupera e exibe informações sobre os valores máximo e mínimo da opção de configuração especificada. Finalmente, o programa informa ao usuário se a alteração foi feita dinamicamente ou se ela foi armazenada até o reinício da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
```powershell
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = Get-Item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {
   "Configuration option has been updated."  
 }  
Else  
 {  
    "Configuration option will be updated when SQL Server is restarted."  
 }  
```  
