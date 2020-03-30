---
title: 'PowerShell: Gerenciar autenticação'
titleSuffix: SQL Server on Linux
description: Saiba como usar o PowerShell para gerenciar a autenticação do Windows e do SQL no SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 22c48323aa7570440a3edb06400d9a96e9bd9924
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75557955"
---
# <a name="powershell-manage-authentication-to-sql-server"></a>PowerShell: Gerenciar a autenticação no SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Por padrão, os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell usam a Autenticação do Windows ao conectar a uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. É possível usar a Autenticação do SQL Server definindo uma unidade virtual do PowerShell ou especificando os parâmetros **-Username** e **-Password** para **Invoke-Sqlcmd**.  
  
> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).

  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Todas as ações que você pode executar em uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] são controladas pelas permissões concedidas às credenciais de autenticação usadas na conexão à instância. Por padrão, o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e cmdlets usam a conta do Windows na qual ele está sendo executado para estabelecer uma conexão de Autenticação do Windows com o [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
 Para fazer uma conexão de Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça uma ID de logon e uma senha de Autenticação do SQL Server. Ao usar o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , associe as credenciais de logon do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a uma unidade virtual e use o comando de alterar diretório (**cd**) para se conectar a essa unidade. No Windows PowerShell, credenciais de segurança só podem ser associadas a unidades virtuais.  
  
##  <a name="sql-server-authentication-using-a-virtual-drive"></a><a name="SQLAuthVirtDrv"></a> Autenticação do SQL Server usando uma unidade virtual  
 **Para criar uma unidade virtual associada com um logon de Autenticação do SQL Server**  
  
1.  Crie uma função que:  
  
    1.  Tenha parâmetros para o nome a ser atribuído à unidade virtual, a ID de logon e o caminho de provedor para associar com a unidade virtual.  
  
    2.  Use **read-host** para solicitar a senha ao usuário.  
  
    3.  Use **new-object** para criar um objeto de credenciais.  
  
    4.  Use **new-psdrive** para criar uma unidade virtual com as credenciais fornecidas.  
  
2.  Chame a função para criar uma unidade virtual com as credenciais fornecidas.  
  
### <a name="example-virtual-drive"></a>Exemplo (Unidade Virtual)  
 Este exemplo cria uma função denominada **sqldrive** que você pode usar para criar uma unidade virtual que é associada ao logon de Autenticação e à instância especificados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 A função **sqldrive** solicita que você insira a senha para seu logon, mascarando a senha à medida que a digita. Então, sempre que você usar o comando de diretório de alteração (**cd**) para se conectar a um caminho usando o nome de unidade virtual, todas as operações serão executadas usando as credenciais de logon de Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que você forneceu ao criar a unidade.  
  
```  
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = read-host -AsSecureString -Prompt "Password"  
    $cred = new-object System.Management.Automation.PSCredential -argumentlist $login,$pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="sql-server-authentication-using-invoke-sqlcmd"></a><a name="SQLAuthInvSqlCmd"></a> Autenticação de SQL Server usando Invoke-Sqlcmd  
 **Para usar Invoke-Sqlcmd com a Autenticação do SQL Server**  
  
1.  Use o parâmetro **-Username** para especificar uma ID de logon e o parâmetro **-Password** para especificar a senha associada.  
  
### <a name="example-invoke-sqlcmd"></a>Exemplo (Invoke-Sqlcmd)  
 Este exemplo usa o cmdlet do host de leitura para solicitar ao usuário uma senha e, depois, conecta usando a Autenticação do SQL Server.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [Provedor do SQL Server PowerShell](sql-server-powershell-provider.md)   
 [cmdlet Invoke-Sqlcmd](invoke-sqlcmd-cmdlet.md)  
  
  
