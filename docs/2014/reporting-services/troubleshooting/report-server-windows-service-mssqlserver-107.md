---
title: Serviço Windows do Servidor de Relatório (MSSQLServer) 107 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
caps.latest.revision: 19
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f5f8f4ab62d893334cfab9020a7cf301e7b7761f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275782"
---
# <a name="report-server-windows-service-mssqlserver-107"></a>Serviço Servidor de Relatório do Windows (MSSQLServer) 107
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|107|  
|Origem do evento|Serviço Servidor de Relatório do Windows|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|O serviço Servidor de Relatório do Windows (MSSQLSERVER) não pode se conectar ao banco de dados do servidor de relatório.|  
  
## <a name="explanation"></a>Explicação  
 O serviço Servidor de Relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar ao banco de dados do servidor de relatório. Esse erro ocorrerá durante a reinicialização do serviço se uma conexão com o banco de dados do servidor de relatório não puder ser estabelecida. As condições em que esse erro ocorre incluem o seguinte:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] não está sendo executado quando o serviço Servidor de Relatório é iniciado.  
  
-   A conexão com o serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] falha porque as conexões remotas ou o protocolo TCP/IP não estão habilitados.  
  
-   O banco de dados do servidor de relatório não está configurado corretamente.  
  
-   A conta de serviço não está configurada corretamente ou a conta já não tem permissões no banco de dados de servidor de relatório. Isso pode ocorrer se você não usar ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar a conta ou o banco de dados do servidor de relatório.  
  
## <a name="user-action"></a>Ação do usuário  
 Inicie o serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] , se ele não estiver em execução ainda, e certifique-se de que as conexões remotas estão habilitadas para o protocolo TCP/IP.  
  
 Use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar o banco de dados do servidor de relatório e a conta do serviço.  
  
## <a name="internal-only"></a>Somente interno  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a conta de serviço do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Gerenciador de configuração do Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Iniciar e parar o serviço Servidor de Relatório](../report-server/start-and-stop-the-report-server-service.md)  
  
  
