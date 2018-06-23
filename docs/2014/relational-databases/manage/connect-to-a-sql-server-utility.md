---
title: Conectar a um Utilitário do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e63feca9bd2cb813da7924d96677f5dcb35ee8eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119333"
---
# <a name="connect-to-a-sql-server-utility"></a>Conectar a um Utilitário do SQL Server
  Para que você possa se conectar a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é necessário criar um UCP (ponto de controle do utilitário). Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](sql-server-utility-features-and-tasks.md).  
  
 Para exibir e gerenciar a integridade de recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectar-se a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para conectar-se a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do SSMS:  
  
1.  Inicie o SSMS.  
  
2.  No SSMS, conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Clique em **Exibir** e em **Gerenciador do Utilitário**.  
  
4.  No painel de navegação do Gerenciador do Utilitário, clique em ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**Conectar ao Utilitário**.  
  
5.  Na caixa de diálogo **Conectar ao Servidor** , especifique o nome da instância UCP e depois clique em **Conectar**.  
  
6.  Exiba o painel de navegação do Gerenciador do Utilitário para ver um modo de exibição de árvore dos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no UCP.  
  
 Criar um novo UCP também conecta ao Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas do Utilitário do SQL Server](sql-server-utility-features-and-tasks.md)   
 [Exibir resultados da política de integridade de recursos &#40;Utilitário do SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md)  
  
  