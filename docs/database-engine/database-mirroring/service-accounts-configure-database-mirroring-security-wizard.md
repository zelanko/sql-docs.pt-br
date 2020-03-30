---
title: 'Assistente para configurar a segurança: Contas de serviço'
description: Descreve a página 'Contas de Serviço' do 'Assistente para Configurar Segurança de Espelhamento de Banco de Dados' no SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8c8a83b68febee5e00a80bd9977713a786b70f9a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822454"
---
# <a name="configure-database-mirroring-security-wizard-service-accounts"></a>Assistente para Configurar Segurança de Espelhamento de Banco de Dados: Contas de serviço
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Configurar contas de logon para espelhamento de banco de dados ou para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
