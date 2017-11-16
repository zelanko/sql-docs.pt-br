---
title: Configurar logs de erros do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aa8816e5496b3dd8689262cffdd07e246ececfb0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="scm-services---configure-sql-server-error-logs"></a>Serviços SCM – configurar logs de erros do SQL Server
  Este tópico descreve como exibir ou modificar o modo como logs de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são reciclados.  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir a caixa de diálogo Configurar Logs de Erros do SQL Server  
  
1.  No Pesquisador de Objetos, expanda a instância do SQL Server, expanda **Gerenciamento**, clique com o botão direito do mouse em **Logs do SQL Server**e clique em **Configurar**.  
  
2.  Na caixa de diálogo **Configurar Logs de Erros do SQL Server** , escolha uma das opções a seguir.  
  
     **Limite o número dos arquivos de log de erros antes que eles sejam reciclados**  
     Verifique e limite o número de logs de erros criados antes que eles sejam reciclados. Um novo log de erros é criado a cada vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém backups dos seis últimos logs, a não ser que essa opção seja marcada um número máximo diferente de arquivos de log de erros seja especificado, logo abaixo.  
  
     **Número máximo de arquivos de log de erros**  
     Especifique o número máximo de arquivos de log de erros criados, antes que eles sejam reciclados. O padrão é 6, que é o número de logs de backup anteriores que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , retém antes de reciclá-los.  
  
  
