---
title: "Contas de serviço (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b1dcb128eb2269265d9439825e163421fa1b3ede
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>Contas de Serviço (Assistente para Configurar Segurança de Espelhamento do Banco de Dados)
  Ao usar a Autenticação do Windows, se as instâncias de servidor usarem contas diferentes, especifique as contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas contas de serviço devem ser todas contas de domínio (nos mesmos domínios ou domínios confiáveis).  
  
 Se todas as instâncias de servidor usarem a mesma conta de domínio ou autenticação com base em certificação, deixe os campos em branco. Basta clicar em **Concluir**e o assistente configurará automaticamente as contas com base na conta do assistente atual.  
  
> [!IMPORTANT]  
>  Se os pontos de extremidade do espelhamento de banco de dados das instâncias de servidor estiverem configurados para usar certificados, então os campos de conta de serviço devem ser deixados em branco.  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Principal**  
 Especifique a conta de serviço da instância de servidor principal. Digite o nome de domínio em letras maiúsculas:  
  
 *DOMAINNAME*\\*nomeusuário*  
  
 **Espelho**  
 Especifique a conta de serviço da instância de servidor espelho. Digite o nome de domínio em letras maiúsculas:  
  
 *DOMAINNAME*\\*nomeusuário*  
  
 **Witness (testemunha)**  
 Especifique a conta de serviço da instância de servidor testemunha. Digite o nome de domínio em letras maiúsculas:  
  
 *DOMAINNAME*\\*nomeusuário*  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Configurar contas de logon para espelhamento de banco de dados ou para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  

