---
title: Criar um ambiente multisservidor
ms.custom: seo-lt-2019
ms.date: 01/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 896b0a435eee20dbe8616e4610e1f51f70cbb4c0
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087541"
---
# <a name="create-a-multiserver-environment"></a>Criar um ambiente multisservidor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A administração multisservidor requer a configuração de um servidor mestre (MSX) e de um ou mais servidores de destino (TSX). Os trabalhos a serem processados em todos os servidores de destino são definidos primeiramente no servidor mestre e depois são baixados nos servidores de destino.  
  
Por padrão, a criptografia TLS completa, anteriormente conhecida como SSL, e a validação de certificado são habilitadas para conexões entre servidores mestres e servidores de destino. Para obter mais informações, veja [Definir opções de criptografia em servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
Se você tiver um número grande de servidores de destino, evite definir seu servidor mestre em um servidor de produção que tenha requisitos de desempenho significantes de outra funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , porque o tráfego do servidor de destino pode reduzir o desempenho em seu servidor de produção. Se também encaminhar eventos a um servidor mestre dedicado, você poderá centralizar a administração em um servidor. Para obter mais informações, consulte [Gerenciar eventos](../../ssms/agent/manage-events.md).  
  
> [!NOTE]  
> Para usar processamento de trabalhos multisservidor, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser membro da função **TargetServersRole** do banco de dados **msdb** no servidor mestre. O Assistente de Servidor Mestre adiciona automaticamente a conta de serviço a essa função como parte do processo de inscrição  
  
## <a name="considerations-for-multiserver-environments"></a>Considerações para ambientes multisservidor  
  
Considere as seguintes questões ao criar um ambiente multisservidor:  
  
-   Use a versão mais recente do servidor mestre. A versão atual e as duas versões anteriores tem suporte.

-   Cada servidor de destino se reporta a apenas um servidor mestre. Você deve remover um servidor de destino de um servidor mestre para poder inscrevê-lo em outro.  
  
-   Para alterar o nome de um servidor de destino, primeiro você deve removê-lo antes de alterar o nome e reinscrevê-lo após a alteração.  
  
-   Se desejar desmontar uma configuração multisservidor, você deve remover todos os servidores de destino do servidor mestre.  
  
-   O SQL Server Integration Services oferece suporte apenas aos servidores de destino que têm a mesma versão ou maior que a versão do servidor mestre.  
  
## <a name="related-tasks"></a>Related Tasks  
Os tópicos a seguir documentam tarefas comuns de criação de um ambiente multisservidor.  
  
|Descrição|Tópico|  
|---------------|---------|  
|Descreve como criar um servidor mestre.|[Criar um servidor mestre](../../ssms/agent/make-a-master-server.md)|  
|Descreve como criar um servidor de destino.|[Criar um servidor de destino](../../ssms/agent/make-a-target-server.md)|  
|Descreve como inscrever um servidor de destino em um servidor mestre.|[Inscrever um servidor de destino em um servidor mestre](../../ssms/agent/enlist-a-target-server-to-a-master-server.md)|  
|Descreve como cancelar a inscrição de um servidor de destino de um servidor mestre.|[Defect a Target Server from a Master Server](../../ssms/agent/defect-a-target-server-from-a-master-server.md)|  
|Descreve como cancelar a inscrição de vários servidores de destino de um servidor mestre.|[Remover vários servidores de destino de um servidor mestre](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)|  
|Descreve como verificar o status de um servidor de destino.|[sp_help_targetserver (Transact-SQL)](https://msdn.microsoft.com/f841d3bd-901a-4980-ad0b-1c6eeba3f717)<br /><br />[sp_help_targetservergroup (Transact-SQL)](https://msdn.microsoft.com/ec3a4a68-b591-431c-9518-053ede522d0c)|  
  
## <a name="see-also"></a>Consulte Também  
[Solucionar problemas de trabalhos com multisservidor que usam proxies](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
