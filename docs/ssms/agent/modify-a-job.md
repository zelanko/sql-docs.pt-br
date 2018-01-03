---
title: Modificar um Trabalho | Microsoft Docs
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
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ecab4d77f591f775926dec6a98e0940750ec070b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="modify-a-job"></a>Modify a Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como alterar as propriedades do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent a categorias de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], o [!INCLUDE[tsql](../../includes/tsql_md.md)] ou o SQL Server Management Objects.  
  
**Neste tópico**  
  
-   **Antes de começar:** ,  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para modificar um trabalho, usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
Um trabalho mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não pode ser destino em ambos os servidores, local e remoto.  
  
### <a name="Security"></a>Segurança  
A menos que seja membro da função de servidor fixa **sysadmin** , você poderá modificar somente trabalhos de sua propriedade. Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>Para modificar um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda o **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja modificar e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , atualize as propriedades, etapas, agenda, alertas e notificações do trabalho, usando as páginas correspondentes.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-modify-a-job"></a>Para modificar um trabalho  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do Mecanismo de Banco de Dados e expanda-a.  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, use os procedimentos armazenados do sistema a seguir para modificar um trabalho.  
  
    -   Executar [sp_update_job (Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623) para alterar os atributos de um trabalho.  
  
    -   Executar [sp_update_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/97b3119b-e43e-447a-bbfb-0b5499e2fefe) para alterar os detalhes do agendamento de uma definição de trabalho.  
  
    -   Execute [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755) para adicionar novas etapas de trabalho.  
  
    -   Execute [sp_update_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b) para alterar etapas de trabalho preexistentes.  
  
    -   Executar [sp_delete_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/421ede8e-ad57-474a-9fb9-92f70a3e77e3) para remover uma etapa de trabalho de um trabalho.  
  
    -   Procedimentos armazenados adicionais para modificar qualquer trabalho mestre do SQL Server Agent:  
  
        -   Execute [sp_delete_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/6d63ed32-68cf-4d8f-aa40-05a3826e05b8) para excluir um servidor atualmente associado a um trabalho.  
  
        -   Execute [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286) para associar um servidor ao trabalho atual.  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para modificar um trabalho**  
  
Use a classe **Job** usando uma linguagem de programação que você possa escolher, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
