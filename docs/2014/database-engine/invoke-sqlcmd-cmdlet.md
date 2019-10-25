---
title: Invoke-Sqlcmd cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], Invoke-Sqlcmd
- Cmdlets [SQL Server], Invoke-Sqlcmd
- Invoke-Sqlcmd cmdlet
- sqlcmd utility, PowerShell
ms.assetid: 0c74d21b-84a5-4fa4-be51-90f0f7230044
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c6aff97c8bee8fe8ccc469c2ee57bc94466e1e31
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797862"
---
# <a name="invoke-sqlcmd-cmdlet"></a>cmdlet Invoke-Sqlcmd
  **Invoke-Sqlcmd** é um cmdlet do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que executa scripts que contêm instruções de linguagem ([!INCLUDE[tsql](../includes/tsql-md.md)] e XQuery) e de comandos que têm suporte do utilitário **sqlcmd**.  
  
## <a name="using-invoke-sqlcmd"></a>Usando Invoke-Sqlcmd  
 O cmdlet **Invoke-Sqlcmd** permite executar arquivos de script **sqlcmd** em um ambiente do Windows PowerShell. Quase tudo o que pode ser feito com **sqlcmd** também pode ser feito com **Invoke-Sqlcmd**.  
  
 Este é um exemplo de uma chamada a Invoke-Sqlcmd para executar uma consulta simples, semelhante à especificação de **sqlcmd** com as opções **-Q** e **-S** :  
  
```powershell
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
 Este é um exemplo de chamada de **Invoke-Sqlcmd**, com a especificação de um arquivo de entrada e o envio da saída para um arquivo. Esse processo é semelhante à especificação de **sqlcmd** com as opções **-i** e **-o** :  
  
```powershell
Invoke-Sqlcmd -InputFile "C:\MyFolder\TestSQLCmd.sql" | Out-File -FilePath "C:\MyFolder\TestSQLCmd.rpt"  
```  
  
 Este é um exemplo do uso de uma matriz do Windows PowerShell para transmitir diversas variáveis de script **sqlcmd** para **Invoke-Sqlcmd**. O caractere "$" que identifica as variáveis de script **sqlcmd** na instrução SELECT foi substituído pelo caractere de escape "`" de continuação de linha do PowerShell:  
  
```powershell
$MyArray = "MyVar1 = 'String1'", "MyVar2 = 'String2'"  
Invoke-Sqlcmd -Query "SELECT `$(MyVar1) AS Var1, `$(MyVar2) AS Var2;" -Variable $MyArray  
```  
  
 Este é um exemplo do uso do provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do Windows PowerShell para navegar por uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]e, em seguida, usar o cmdlet **Get-Item** do Windows PowerShell para recuperar o objeto Servidor SMO da instância e passá-lo para o **Invoke-Sqlcmd**:  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\MyInstance  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance (Get-Item .)  
```  
  
 O parâmetro -Query é posicional e não precisa ser nomeado. Se a primeira cadeia de caracteres transmitida para **Invoke-Sqlcmd**: não for nomeada, ela será tratada como o parâmetro -Query.  
  
```powershell
Invoke-Sqlcmd "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
## <a name="path-context-in-invoke-sqlcmd"></a>Contexto de caminho em Invoke-Sqlcmd  
 Se você não usar o parâmetro -Database, o contexto do banco de dados para Invoke-Sqlcmd será definido pelo caminho que estiver ativo quando o cmdlet for chamado.  
  
|demarcador|Contexto do Banco de Dados|  
|----------|----------------------|  
|Inicia com uma unidade diferente de SQLSERVER:|O banco de dados padrão para a identificação de logon na instância padrão no computador local.|  
|SQLSERVER:\SQL|O banco de dados padrão para a identificação de logon na instância padrão no computador local.|  
|SQLSERVER:\SQL\ComputerName|O banco de dados padrão para a identificação de logon na instância padrão no computador especificado.|  
|SQLSERVER:\SQL\ComputerName\InstanceName|O banco de dados padrão para a identificação de logon na instância especificada no computador especificado.|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases|O banco de dados padrão para a identificação de logon na instância especificada no computador especificado.|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases\DatabaseName|O banco de dados especificado na instância especificada no computador especificado. Isto também se aplica a caminhos mais longos, como um caminho que especifica os nós Tabelas e Colunas dentro de um banco de dados.|  
  
 Por exemplo, assuma que o banco de dados padrão para sua conta de Windows na instância padrão do computador local é mestre. Então, os seguintes comandos retornariam mestre:  
  
```powershell
Set-Location SQLSERVER:\SQL  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 Os comandos a seguir retornariam [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]:  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Person  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 Invoke-Sqlcmd fornece um aviso quando usa o contexto do banco de dados de caminho. Você pode usar o parâmetro -SuppressProviderContextWarning para desativar a mensagem de aviso. Você pode usar o parâmetro -IgnoreProviderContext para pedir que Invoke-Sqlcmd use sempre o banco de dados padrão para logon.  
  
## <a name="comparing-invoke-sqlcmd-and-the-sqlcmd-utility"></a>Comparando o Invoke-Sqlcmd e o utilitário sqlcmd  
 **Invoke-Sqlcmd** pode ser usado para executar muitos dos scripts que podem ser executados com o utilitário **sqlcmd** . Porém, **Invoke-Sqlcmd** executa em um ambiente do Windows PowerShell que é diferente do ambiente de prompt de comando em que **sqlcmd** é executado. O comportamento de **Invoke-Sqlcmd** foi modificado para funcionar em um ambiente do Windows PowerShell.  
  
 Nem todos os comandos **sqlcmd** são implementados no **Invoke-Sqlcmd**. Os comandos que não são implementados incluem o seguinte: **:!!** , **:connect**, **:error**, **:out**, **:ed**, **:list**, **:listvar**, **:reset**, **:perftrace**e **:serverlist**.  
  
 **Invoke-Sqlcmd** não inicializa o ambiente **sqlcmd** ou variáveis de scripts como SQLCMDDBNAME ou SQLCMDWORKSTATION.  
  
 **Invoke-Sqlcmd** não exibe mensagens, como a saída de instruções PRINT, a menos que você especifique o parâmetro comum **-Verbose** do Windows PowerShell. Por exemplo:  
  
```powershell
Invoke-Sqlcmd -Query "PRINT N'abc';" -Verbose  
```  
  
 Nem todos os parâmetros **sqlcmd** são necessários em um ambiente do PowerShell. Por exemplo, o Windows PowerShell formata todas as saídas dos cmdlets, de modo que as opções de formatação de especificação de parâmetros **sqlcmd** não sejam implementadas no **Invoke-Sqlcmd**. A tabela a seguir mostra o relacionamento entre os parâmetros **Invoke-Sqlcmd** e as opções **sqlcmd** :  
  
|Description|Opção sqlcmd|Parâmetro Invoke-Sqlcmd|  
|-----------------|-------------------|------------------------------|  
|Nome do servidor e da instância.|-S|-ServerInstance|  
|O banco de dados inicial a ser usado.|-d|-Database|  
|Executar a consulta especificada e sair.|-Q|-Query|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ID de logon para Autenticação.|-U|-Username|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Senha de autenticação.|-p|-Password|  
|Definição de variável.|-V|-Variable|  
|Intervalo de tempo limite da consulta.|-T|-QueryTimeout|  
|Interromper a execução em um erro|-b|-AbortOnError|  
|Conexão de Administrador Dedicada.|-a|-DedicatedAdministratorConnection|  
|Desabilitar comandos interativos, script de inicialização e variáveis de ambiente.|-X|-DisableCommands|  
|Desabilitar substituição de variável.|-X|-DisableVariables|  
|Nível de severidade mínimo a ser informado.|-v|-SeverityLevel|  
|Nível de erro mínimo a ser informado.|-M|-ErrorLevel|  
|Intervalo de tempo limite de logon.|-l|-ConnectionTimeout|  
|Hostname.|-H|-HostName|  
|Alterar senha e sair.|-Z|-NewPassword|  
|Arquivo de entrada que contém uma consulta|-i|-InputFile|  
|Comprimento máximo de saída de caracteres.|-w|-MaxCharLength|  
|Comprimento máximo de saída binária.|-w|-MaxBinaryLength|  
|Estabelecer conexão com criptografia SSL.|Sem parâmetros|-EncryptConnection|  
|Exibir erros|Sem parâmetros|-OutputSqlErrors|  
|Produzir mensagens para stderr.|-r|Sem parâmetros|  
|Usar configurações regionais do cliente|-r|Sem parâmetros|  
|Executar a consulta especificada e continuar executando.|-Q|Sem parâmetros|  
|Página de código a ser usada para obter dados de saída.|-f|Sem parâmetros|  
|Alterar uma senha e continuar executando.|-Z|Sem parâmetros|  
|Tamanho do pacote|-A|Sem parâmetros|  
|Separador de coluna|-S|Sem parâmetros|  
|Cabeçalhos de saída de controle|-H|Sem parâmetros|  
|Especificar caracteres de controle|-k|Sem parâmetros|  
|Largura da exibição de comprimento fixo|-y|Sem parâmetros|  
|Largura da exibição de comprimento variável|-y|Sem parâmetros|  
|Entrada de eco|-E|Sem parâmetros|  
|Habilitar identificadores entres aspas|-i|Sem parâmetros|  
|Remover espaços à direita|-w|Sem parâmetros|  
|Listar instâncias|-l|Sem parâmetros|  
|Formatar saída como Unicode|-U|Sem parâmetros|  
|Imprimir estatísticas|-P|Sem parâmetros|  
|Término de comando|-c|Sem parâmetros|  
|Conectar usando a Autenticação do Windows|-E|Sem parâmetros|  
  
## <a name="see-also"></a>Consulte Também  
 [Usar cmdlets do Mecanismo de Banco de Dados](../../2014/database-engine/use-the-database-engine-cmdlets.md)   
 [sqlcmd Utility](../tools/sqlcmd-utility.md)   
 [Usar o utilitário sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
