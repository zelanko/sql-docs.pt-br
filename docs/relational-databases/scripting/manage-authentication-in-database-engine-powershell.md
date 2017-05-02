---
title: "Gerenciar a autenticação no PowerShell do Mecanismo de Banco de Dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 135580dd67315ad9eb07361dcff7b1334398a0aa
ms.lasthandoff: 04/11/2017

---
# <a name="manage-authentication-in-database-engine-powershell"></a>Gerenciar a autenticação no Mecanismo de Banco de Dados com o PowerShell
  Por padrão, os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell usam a Autenticação do Windows ao conectar a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Você pode usar a Autenticação do SQL Server definindo uma unidade virtual do PowerShell ou especificando os parâmetros **–Username** e **–Password** para **Invoke-Sqlcmd**.  
  
1.  **Before you begin:**  [Permissions](#Permissions)  
  
2.  **To set authentication, using:**  [A Virtual Drive](#SQLAuthVirtDrv), [Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="Permissions"></a> Permissões  
 Todas as ações que você pode executar em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são controladas pelas permissões concedidas às credenciais de autenticação usadas na conexão à instância. Por padrão, o provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e cmdlets usam a conta do Windows na qual ele está sendo executado para estabelecer uma conexão de Autenticação do Windows com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Para fazer uma conexão de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , forneça uma ID de logon e uma senha de Autenticação do SQL Server. Ao usar o provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , associe as credenciais de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a uma unidade virtual e use o comando de alterar diretório (**cd**) para se conectar a essa unidade. No Windows PowerShell, credenciais de segurança só podem ser associadas a unidades virtuais.  
  
##  <a name="SQLAuthVirtDrv"></a> Autenticação do SQL Server usando uma unidade virtual  
 **Para criar uma unidade virtual associada com um logon de Autenticação do SQL Server**  
  
1.  Crie uma função que:  
  
    1.  Tenha parâmetros para o nome a ser atribuído à unidade virtual, a ID de logon e o caminho de provedor para associar com a unidade virtual.  
  
    2.  Use **read-host** para solicitar a senha ao usuário.  
  
    3.  Use **new-object** para criar um objeto de credenciais.  
  
    4.  Use **new-psdrive** para criar uma unidade virtual com as credenciais fornecidas.  
  
2.  Chame a função para criar uma unidade virtual com as credenciais fornecidas.  
  
### <a name="example-virtual-drive"></a>Exemplo (Unidade Virtual)  
 Este exemplo cria uma função denominada **sqldrive** que você pode usar para criar uma unidade virtual que é associada ao logon de Autenticação e à instância especificados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A função **sqldrive** solicita que você insira a senha para seu logon, mascarando a senha à medida que a digita. Então, sempre que você usar o comando de diretório de alteração (**cd**) para se conectar a um caminho usando o nome de unidade virtual, todas as operações serão executadas usando as credenciais de logon de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você forneceu ao criar a unidade.  
  
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
  
##  <a name="SQLAuthInvSqlCmd"></a> Autenticação de SQL Server usando Invoke-Sqlcmd  
 **Para usar Invoke-Sqlcmd com a Autenticação do SQL Server**  
  
1.  Use o parâmetro **–Username** para especificar uma ID de logon e o parâmetro **–Password** para especificar a senha associada.  
  
### <a name="example-invoke-sqlcmd"></a>Exemplo (Invoke-Sqlcmd)  
 Este exemplo usa o cmdlet do host de leitura para solicitar ao usuário uma senha e, depois, conecta usando a Autenticação do SQL Server.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" –Username “MyLogin” –Password $pwd  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [cmdlet Invoke-Sqlcmd](../../powershell/invoke-sqlcmd-cmdlet.md)  
  
  
