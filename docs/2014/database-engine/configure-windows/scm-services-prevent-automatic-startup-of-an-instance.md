---
title: Impedir a inicialização automática de uma instância do SQL Server (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b21ac71b54c9bfee76079f86c1d6d1a32fc0f9dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008706"
---
# <a name="prevent-automatic-startup-of-an-instance-of-sql-server-sql-server-configuration-manager"></a>Impedir a inicialização automática de uma instância do SQL Server (SQL Server Configuration Manager)
  Este tópico descreve como impedir que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicie automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é normalmente configurado para iniciar automaticamente. Você pode alterar isso definindo o modo de início da instância como manual.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>Para evitar a inicialização automática de uma instância do SQL Server  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No SQL Server Configuration Manager, expanda **Serviços**e clique em **SQL Server**.  
  
3.  No painel detalhes, clique com o botão direito do mouse em **MSSQLServer**e clique em **Propriedades.**  
  
4.  No **do SQL Server \< ***instancename***> propriedades** na caixa de **propriedades** caixa, defina o valor de **modo inicial**para **Manual**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Propriedades de \<***instancename***> do SQL Server** e, em seguida, feche o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)  
  
  