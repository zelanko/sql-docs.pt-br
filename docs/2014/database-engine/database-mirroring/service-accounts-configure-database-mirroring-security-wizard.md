---
title: Contas de serviço (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fdca44263bfa60ebf7a2a2a3d66d0c827c3d0868
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120643"
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>Contas de Serviço (Assistente para Configurar Segurança de Espelhamento do Banco de Dados)
  Ao usar a Autenticação do Windows, se as instâncias de servidor usarem contas diferentes, especifique as contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas contas de serviço devem ser todas contas de domínio (nos mesmos domínios ou domínios confiáveis).  
  
 Se todas as instâncias de servidor usarem a mesma conta de domínio ou autenticação com base em certificação, deixe os campos em branco. Basta clicar em **Concluir**e o assistente configurará automaticamente as contas com base na conta do assistente atual.  
  
> [!IMPORTANT]  
>  Se os pontos de extremidade do espelhamento de banco de dados das instâncias de servidor estiverem configurados para usar certificados, então os campos de conta de serviço devem ser deixados em branco.  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
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
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Configurar contas de logon para espelhamento de banco de dados ou grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  