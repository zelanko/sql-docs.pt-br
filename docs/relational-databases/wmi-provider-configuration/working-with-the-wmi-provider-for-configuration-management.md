---
title: Usar o provedor WMI para o gerenciamento de configuração
description: Saiba mais sobre o provedor WMI para gerenciamento de configuração, incluindo associação, especificação de uma cadeia de conexão e permissões/autenticação de servidor.
ms.custom: seo-lt-2019
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
ms.openlocfilehash: da0f68133473e746b7eaae898273b3c8a8bab0cd
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880458"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Trabalhando com o provedor WMI para o Gerenciamento de configuração

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo fornece orientação sobre como programar com o provedor WMI para gerenciamento do computador.

## <a name="binding"></a>Associação  
 O provedor WMI para gerenciamento de configuração é um modelo de objeto COM que dá suporte a associações iniciais e tardias. Com a associação tardia, você pode usar linguagens de script, como o VBScript, para manipular, de forma programada, os serviços, as configurações de rede e os aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="specifying-a-connection-string"></a>Especificando uma cadeia de caracteres de conexão

Os aplicativos direcionam o provedor WMI para gerenciamento de configuração para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando a um namespace WMI definido pelo provedor. O serviço WMI do Windows mapeia esse namespace para a DLL do provedor e carrega a DLL na memória. Todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são representadas com um único namespace WMI.

O namespace usa como padrão o formato a seguir. No formato, `VV` é o número de versão principal do SQL Server. O número é detectável pela execução `SELECT @@VERSION;` .

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

Quando você se conecta usando o PowerShell, a entrelinha `\\.\` deve ser removida. Por exemplo, o código do PowerShell a seguir lista todas as classes WMI para um SQL Server 2016, que é a versão principal 13.

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

Você pode usar o código do PowerShell a seguir para consultar todos os namespaces do WMI ComputerManagement disponíveis.

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **Observação:** Se você estiver se conectando por meio do firewall do Windows, precisará verificar se os computadores estão configurados corretamente. Consulte o artigo "conectando por meio do firewall do Windows" na documentação do Instrumentação de Gerenciamento do Windows no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [site](https://go.microsoft.com/fwlink/?linkid=15426)do MSDN.  
  
## <a name="permissions-and-server-authentication"></a>Permissões e autenticação do servidor  
 Para acessar o provedor WMI para gerenciamento de configuração, o script de gerenciamento WMI do cliente deve estar sendo executado no contexto de um administrador no computador de destino. Você precisa ser membro do grupo local de administradores do Windows no computador que deseja gerenciar.  
  
 O administrador pode definir políticas de grupo para controlar o acesso de usuários aos provedores WMI. Para obter mais informações sobre como definir políticas de grupo, consulte "Group Policy and MMC" na ajuda do Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O script de gerenciamento WMI pode ser usado para atualizar a conta na qual os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados.  
  
 Os certificados de segurança são suportados pelo provedor WMI para gerenciamento de configuração. Para obter mais informações sobre certificados, consulte [hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
