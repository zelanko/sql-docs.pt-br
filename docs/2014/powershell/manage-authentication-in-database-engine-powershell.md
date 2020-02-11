---
title: Gerenciar a autenticação no PowerShell do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a04e581758748d55b9defcab3beaa6a86f0eecf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797800"
---
# <a name="manage-authentication-in-database-engine-powershell"></a>Gerenciar a autenticação no Mecanismo de Banco de Dados com o PowerShell
  Por padrão, os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell usam a Autenticação do Windows ao conectar a uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Você pode usar a Autenticação do SQL Server, definindo uma unidade virtual do PowerShell ou especificando os parâmetros `-Username` e `-Password` para `Invoke-Sqlcmd`.  
  
1.  **Antes de começar:**  [permissões](#Permissions)  
  
2.  **Para definir a autenticação usando:**  [uma unidade virtual](#SQLAuthVirtDrv), [Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="Permissions"></a> Permissões  
 Todas as ações que você pode executar em uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] são controladas pelas permissões concedidas às credenciais de autenticação usadas na conexão à instância. Por padrão, o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e cmdlets usam a conta do Windows na qual ele está sendo executado para estabelecer uma conexão de Autenticação do Windows com o [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
 Para fazer uma conexão de Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça uma ID de logon e uma senha de Autenticação do SQL Server. Ao usar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] provedor, você deve associar as [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] credenciais de logon a uma unidade virtual e, em seguida, usar o comando`cd`Change Directory () para se conectar a essa unidade. No Windows PowerShell, credenciais de segurança só podem ser associadas a unidades virtuais.  
  
##  <a name="SQLAuthVirtDrv"></a>SQL Server autenticação usando uma unidade virtual  
 **Para criar uma unidade virtual associada a um logon SQL Server autenticação**  
  
1.  Crie uma função que:  
  
    1.  Tenha parâmetros para o nome a ser atribuído à unidade virtual, a ID de logon e o caminho de provedor para associar com a unidade virtual.  
  
    2.  Usa `read-host` para solicitar a senha do usuário.  
  
    3.  Usa `new-object` para criar um objeto de credenciais.  
  
    4.  Usa `new-psdrive` para criar uma unidade virtual com as credenciais fornecidas.  
  
2.  Chame a função para criar uma unidade virtual com as credenciais fornecidas.  
  
### <a name="example-virtual-drive"></a>Exemplo (Unidade Virtual)  
 Este exemplo cria uma função denominada **sqldrive** que você pode usar para criar uma unidade virtual que é associada ao logon de Autenticação e à instância especificados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 A função **sqldrive** solicita que você insira a senha para seu logon, mascarando a senha à medida que a digita. Em seguida, sempre que você usar o comando Change`cd`Directory () para se conectar a um caminho usando o nome da unidade virtual, todas as operações serão [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] executadas usando as credenciais de logon de autenticação que você forneceu quando criou a unidade.  
  
```powershell
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = Read-Host -AsSecureString -Prompt "Password"  
    $cred = New-Object System.Management.Automation.PSCredential -argumentlist $login, $pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a>Autenticação SQL Server usando Invoke-Sqlcmd  
 **Para usar Invoke-Sqlcmd com autenticação SQL Server**  
  
1.  Use o parâmetro `-Username` para especificar uma ID de logon e o parâmetro `-Password` para especificar a senha associada.  
  
### <a name="example-invoke-sqlcmd"></a>Exemplo (Invoke-Sqlcmd)  
 Este exemplo usa o cmdlet do host de leitura para solicitar ao usuário uma senha e, depois, conecta usando a Autenticação do SQL Server.  
  
```powershell
## Prompt the user for their password.  
$pwd = Read-Host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [Provedor de SQL Server PowerShell](sql-server-powershell-provider.md)   
 [cmdlet Invoke-Sqlcmd](../database-engine/invoke-sqlcmd-cmdlet.md)  
