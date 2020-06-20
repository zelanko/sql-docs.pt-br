---
title: Impedir a inicialização automática de uma instância do SQL Server (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8f93f5abc749f589ab4208b3a4c9434ca63b8769
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935027"
---
# <a name="prevent-automatic-startup-of-an-instance-of-sql-server-sql-server-configuration-manager"></a>Impedir a inicialização automática de uma instância do SQL Server (SQL Server Configuration Manager)
  Este tópico descreve como impedir que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicie automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é normalmente configurado para iniciar automaticamente. Você pode alterar isso definindo o modo de início da instância como manual.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>Para evitar a inicialização automática de uma instância do SQL Server  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  Em SQL Server Configuration Manager, expanda **Serviços**e clique em **SQL Server**.  
  
3.  No painel detalhes, clique com o botão direito do mouse em **MSSQLServer**e clique em **Propriedades.**  
  
4.  Na caixa de diálogo ** \<**_instancename_**> propriedades do SQL Server** , na **caixa Propriedades** , defina o valor do **modo de início** como **manual**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo ** \<**_instancename_**> Propriedades do SQL Server** e feche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
