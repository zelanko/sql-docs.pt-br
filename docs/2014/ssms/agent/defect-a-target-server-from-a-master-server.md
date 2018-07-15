---
title: Remover um servidor de destino de um servidor mestre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 35f113cfd0e038940c00b710b31f254da6343805
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37305036"
---
# <a name="defect-a-target-server-from-a-master-server"></a>Remover um servidor de destino de um servidor mestre
  Este tópico descreve como remover um servidor de destino de um servidor mestre no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SQL Server Management Objects (SMO). Execute este procedimento a partir do servidor de destino.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para remover um servidor de destino usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa `sysadmin`.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para remover um servidor de destino de um servidor mestre  
  
1.  No **Pesquisador de Objetos**, expanda um servidor que esteja configurado como servidor de destino.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Remover**.  
  
3.  Clique em **Sim** para confirmar que deseja remover o servidor de destino de um servidor mestre.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para remover um servidor de destino de um servidor mestre  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
```  
sp_msx_defect ;  
```  
  
 Para obter mais informações, consulte [sp_msx_defect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-defect-transact-sql).  
  
##  <a name="PowerShellProcedure"></a> Usando o SQL Server Management Objects (SMO)  
 Use a `MsxDefect Method`.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um ambiente multisservidor](create-a-multiserver-environment.md)   
 [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)   
 [Remover vários servidores de destino de um servidor mestre](defect-multiple-target-servers-from-a-master-server.md)  
  
  
