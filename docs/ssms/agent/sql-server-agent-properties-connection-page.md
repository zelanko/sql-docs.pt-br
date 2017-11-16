---
title: "Propriedades do SQL Server Agent (página Conexão) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d7cbddb41ee84f0525820980639de631b2033db
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-agent-properties-connection-page"></a>Propriedades do SQL Server Agent (página Conexão)
Use esta página para exibir e modificar as configurações da conexão do serviço [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opções  
**Servidor de host local do alias**  
Especifica o alias a ser usado para se conectar à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você não puder usar as opções de conexão padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, defina um alias para a instância e especifique o alias aqui.  
  
**Usar Autenticação do Windows**  
Define a autenticação do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows como o método de autenticação usado para conectar-se com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent conecta-se como a conta com que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é executado.  
  
**Usar Autenticação do SQL Server**  
Define a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como o método de autenticação usado para conectar-se com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] A autenticação é fornecida para fins de compatibilidade com versões anteriores. Para maior segurança, use a autenticação do Windows, se possível.  
  
**Logon**  
Especifica o nome de logon a ser usado para conectar-se com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Senha**  
Especifica a senha a ser usada para conectar-se com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
