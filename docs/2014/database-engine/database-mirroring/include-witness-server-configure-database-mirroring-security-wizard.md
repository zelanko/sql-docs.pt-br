---
title: Incluir servidor testemunha (Assistente para Configurar Segurança de Espelhamento do Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.inclwitness.f1
ms.assetid: f04b38a4-f4e2-4d4c-bdac-7cc70e5a5684
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 57d476216b34053f6bb61deef719d082240ca0c8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934147"
---
# <a name="include-witness-server-configure-database-mirroring-security-wizard"></a>Incluir servidor testemunha (Assistente para Configurar Segurança de Espelhamento do Banco de Dados)
  Use essa página para especificar se você deseja incluir um servidor testemunha nessa configuração de segurança para espelhamento de banco de dados.  
  
 **Para configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opções  
 **Sim**  
 Clique para incluir uma instância de servidor testemunha na configuração de segurança. A testemunha é necessária para o modo de alta segurança com failover automático, que oferece suporte para failover automático para a instância do servidor espelho se a instância do servidor principal falhar.  
  
 **Não**  
 Clique para configurar a segurança sem uma testemunha.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do banco de dados &#40;página espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [SQL Server de espelhamento de banco de dados &#40;&#41;](database-mirroring-sql-server.md)   
 [Testemunha de espelhamento de banco de dados](database-mirroring-witness.md)  
  
  
