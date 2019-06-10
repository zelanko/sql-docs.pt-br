---
title: Escolher os servidores a serem configurados (Assistente para Configurar Segurança de Espelhamento de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 31c9ce74c6638925b1a91ab6d63abb8c759324cf
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774954"
---
# <a name="choose-servers-to-configure-configure-database-mirroring-security-wizard"></a>Selecionar servidores a configurar (Assistente para Configurar Segurança de Espelhamento de Banco de Dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use essa página para especificar quais instâncias de servidor serão configuradas no momento. É preciso selecionar no mínimo uma instância de servidor antes de prosseguir com o assistente.  
  
 Se você desmarcar a caixa de seleção de uma instância de servidor, o assistente não fará nenhuma alteração nessa instância. O assistente, porém, solicitará que você insira informações sobre essa instância e salvará as informações como parte da configuração das outras instâncias de servidor. Por exemplo, se você desmarcar a caixa de seleção da instância de servidor testemunha, o assistente solicitará a inserção da conta de serviços da testemunha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , uma vez que um logon para essa conta precisará ser criado como parte da configuração de segurança salva nas instâncias do servidor principal e de espelhamento.  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Instância do servidor principal**  
 Selecione para configurar a segurança do servidor principal.  
  
 **Instância do servidor espelho**  
 Selecione para configurar a segurança do servidor espelho.  
  
 **Instância do servidor testemunha**  
 Selecione para configurar segurança para o servidor testemunha (se houver).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
