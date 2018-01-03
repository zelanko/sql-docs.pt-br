---
title: "Designar um operador à prova de falhas | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66427475aa5ba8bf49ba8a0310b120be97556b3f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="designate-a-fail-safe-operator"></a>Designar um operador à prova de falhas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Um operador à prova de falhas é um usuário que recebe o alerta caso não seja possível localizar o operador designado. Este tópico descreve como configurar um operador à prova de falhas para receber notificações de alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para designar um operador à prova de falhas usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   Observe que o SQL Server Agent deve ser configurado para usar o Database Mail a fim de enviar notificações por pager ou email a operadores. Para obter mais informações, consulte [Atribuir alertas a um operador](http://msdn.microsoft.com/library/ms190038.aspx).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Somente membros da função de servidor fixa **sysadmin** podem designar operadores à prova de falhas.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>Para designar um operador à prova de falhas  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor contém operador do SQL Server Agent que você deseja designar como à prova de falhas.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent –***server_name* , em **Selecionar uma página**, selecione **Sistema de Alerta**.  
  
4.  Em **Operador à prova de falhas**, selecione **Habilitar operador à prova de falhas**.  
  
5.  Na lista **Operador** , selecione o operador que você deseja tornar à prova de falhas.  
  
6.  Marque qualquer uma ou todas as caixas de seleção a seguir para especificar como o operador será notificado: **Email**, **Pager**ou **Net send**.  
  
7.  Quando terminar, clique em **OK**.  
  
