---
title: "Trabalhando com o provedor WMI para gerenciamento de configuração | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 672720d9c807d2b8eef78a5c0f0b3865679738bb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Trabalhando com o provedor WMI para o Gerenciamento de configuração
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Considere o seguinte antes de programar com o provedor WMI para gerenciamento do computador:  
  
## <a name="binding"></a>Associação  
 O provedor WMI para gerenciamento de configuração é um modelo de objeto COM que dá suporte a associações iniciais e tardias. Com a associação tardia, você pode usar linguagens de script, como o VBScript, para manipular, de forma programada, os serviços, as configurações de rede e os aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como programar as implementações do provedor WMI usando linguagens de script, consulte o [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [site da Web](http://go.microsoft.com/fwlink/?linkid=15426).  
  
## <a name="specifying-a-connection-string"></a>Especificando uma cadeia de caracteres de conexão  
 Os aplicativos direcionam o provedor WMI para gerenciamento de configuração para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando a um namespace WMI definido pelo provedor. O serviço Windows WMI mapeia esse namespace para a DLL do provedor e o carrega na memória. Todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são representadas com um único namespace WMI. O namespace assume este padrão  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 onde `instance_name` assume `MSSQLSERVER` como padrão em uma instalação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Observação:** se você estiver se conectando através do Firewall do Windows você precisará certificar-se de que seus computadores estejam configurados adequadamente. Consulte o artigo "Connecting Through Windows Firewall" na documentação do Windows Management Instrumentation no [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [site da Web](http://go.microsoft.com/fwlink/?linkid=15426).  
  
## <a name="permissions-and-server-authentication"></a>Permissões e autenticação do servidor  
 Para acessar o provedor WMI para gerenciamento de configuração, o script de gerenciamento WMI do cliente deve estar sendo executado no contexto de um administrador no computador de destino. Você precisa ser membro do grupo local de administradores do Windows no computador que deseja gerenciar.  
  
 O administrador pode definir políticas de grupo para controlar o acesso de usuários aos provedores WMI. Para obter mais informações sobre como definir políticas de grupo, consulte "Group Policy and MMC" na ajuda do Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O script de gerenciamento WMI pode ser usado para atualizar a conta na qual os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados.  
  
 Os certificados de segurança são suportados pelo provedor WMI para gerenciamento de configuração. Para obter mais informações sobre certificados, consulte [hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
