---
title: Trabalhando com o provedor WMI para gerenciamento de configuração | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e6736c73f7cda435d91e3ec9c9f523bdc08f1b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139275"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Trabalhando com o provedor WMI para o Gerenciamento de configuração

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Este artigo fornece orientação sobre como programar com o provedor WMI para gerenciamento do computador.

## <a name="binding"></a>Associação  
 O provedor WMI para gerenciamento de configuração é um modelo de objeto COM que dá suporte a associações iniciais e tardias. Com a associação tardia, você pode usar linguagens de script, como o VBScript, para manipular, de forma programada, os serviços, as configurações de rede e os aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="specifying-a-connection-string"></a>Especificando uma cadeia de caracteres de conexão

Os aplicativos direcionam o provedor WMI para gerenciamento de configuração para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando a um namespace WMI definido pelo provedor. O serviço Windows WMI mapeia esse namespace para a DLL do provedor e carrega a DLL na memória. Todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são representadas com um único namespace WMI.

O namespace padrão é o formato a seguir. O formato, `VV` é o número de versão principal do SQL Server. O número é detectável executando `SELECT @@VERSION;`.

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

Quando você se conectar usando o PowerShell, o entrelinhamento `\\.\` devem ser removidos. Por exemplo, o código do PowerShell a seguir lista todas as classes WMI do SQL Server 2016, que é a versão principal 13.

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

Você pode usar o seguinte código do PowerShell para consultar todos os namespaces WMI ComputerManagement disponíveis.

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **Observação:** Se você estiver se conectando através do Firewall do Windows, você precisará certificar-se de que seus computadores estejam configurados adequadamente. Consulte o artigo "Conectando através do Windows Firewall" na documentação da instrumentação de gerenciamento do Windows no [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [site da Web](https://go.microsoft.com/fwlink/?linkid=15426).  
  
## <a name="permissions-and-server-authentication"></a>Permissões e autenticação do servidor  
 Para acessar o provedor WMI para gerenciamento de configuração, o script de gerenciamento WMI do cliente deve estar sendo executado no contexto de um administrador no computador de destino. Você precisa ser membro do grupo local de administradores do Windows no computador que deseja gerenciar.  
  
 O administrador pode definir políticas de grupo para controlar o acesso de usuários aos provedores WMI. Para obter mais informações sobre como definir políticas de grupo, consulte "Group Policy and MMC" na ajuda do Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O script de gerenciamento WMI pode ser usado para atualizar a conta na qual os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados.  
  
 Os certificados de segurança são suportados pelo provedor WMI para gerenciamento de configuração. Para obter mais informações sobre certificados, consulte [hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
