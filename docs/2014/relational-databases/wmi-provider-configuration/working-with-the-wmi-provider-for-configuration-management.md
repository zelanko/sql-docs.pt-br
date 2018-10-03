---
title: Trabalhando com o provedor WMI para gerenciamento de configuração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
manager: craigg
ms.openlocfilehash: c2722d608b4f373de92c49f1d75b887c658417e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183227"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Trabalhando com o provedor WMI para o Gerenciamento de configuração
  Considere o seguinte antes de programar com o provedor WMI para Gerenciamento do Computador:  
  
## <a name="binding"></a>Associação  
 O provedor WMI para gerenciamento de configuração é um modelo de objeto COM que dá suporte a associações iniciais e tardias. Com a associação tardia, você pode usar linguagens de script, como o VBScript, para manipular, de forma programada, os serviços, as configurações de rede e os aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como programar as implementações do provedor de WMI usando linguagens de script, consulte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [site da Web](http://go.microsoft.com/fwlink/?linkid=15426).  
  
## <a name="specifying-a-connection-string"></a>Especificando uma cadeia de caracteres de conexão  
 Os aplicativos direcionam o provedor WMI para gerenciamento de configuração para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando a um namespace WMI definido pelo provedor. O serviço Windows WMI mapeia esse namespace para a DLL do provedor e o carrega na memória. Todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são representadas com um único namespace WMI. O namespace assume este padrão  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 onde `instance_name` assume `MSSQLSERVER` como padrão em uma instalação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Observação:** se você estiver se conectando através do Firewall do Windows que você precisará certificar-se de que seus computadores estejam configurados adequadamente. Consulte o artigo "Conectando através do Windows Firewall" na documentação da instrumentação de gerenciamento do Windows no [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [site da Web](http://go.microsoft.com/fwlink/?linkid=15426).  
  
## <a name="permissions-and-server-authentication"></a>Permissões e autenticação do servidor  
 Para acessar o provedor WMI para gerenciamento de configuração, o script de gerenciamento WMI do cliente deve estar sendo executado no contexto de um administrador no computador de destino. Você precisa ser membro do grupo local de administradores do Windows no computador que deseja gerenciar.  
  
 O administrador pode definir políticas de grupo para controlar o acesso de usuários aos provedores WMI. Para obter mais informações sobre como definir políticas de grupo, consulte "Group Policy and MMC" na ajuda do Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O script de gerenciamento WMI pode ser usado para atualizar a conta na qual os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados.  
  
 Os certificados de segurança são suportados pelo provedor WMI para gerenciamento de configuração. Para obter mais informações sobre certificados, consulte [hierarquia de criptografia](../security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)  
  
  
