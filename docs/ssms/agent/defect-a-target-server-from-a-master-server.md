---
title: Remover um servidor de destino de um servidor mestre | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ff02e4d5b98ef7a17956d401b3a40882cc6cc15
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="defect-a-target-server-from-a-master-server"></a>Defect a Target Server from a Master Server
Este tópico descreve como remover um servidor de destino de um servidor mestre no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]ou SQL Server Management Objects (SMO). Execute este procedimento a partir do servidor de destino.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para remover um servidor de destino usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SMO](#PowerShellProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para remover um servidor de destino de um servidor mestre  
  
1.  No **Pesquisador de Objetos**, expanda um servidor que esteja configurado como servidor de destino.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Remover**.  
  
3.  Clique em **Sim** para confirmar que deseja remover o servidor de destino de um servidor mestre.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para remover um servidor de destino de um servidor mestre  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
sp_msx_defect ;  
```  
  
Para obter mais informações, veja [sp_msx_defect (Transact-SQL)](http://msdn.microsoft.com/en-us/0dfd963a-3bc5-4b58-94f7-aec976da2883).  
  
## <a name="PowerShellProcedure"></a>Usando o SMO (SQL Server Management Objects)  
Use o **método MsxDefect**.  
  
## <a name="see-also"></a>Consulte também  
[Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md)  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Remover vários servidores de destino de um servidor mestre](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
