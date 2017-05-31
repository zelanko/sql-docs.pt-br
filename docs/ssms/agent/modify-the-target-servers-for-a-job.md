---
title: Modificar os servidores de destino de um trabalho | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a3e071ed87ccd53b805b5132c861cb3dc8b530ea
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="modify-the-target-servers-for-a-job"></a>Modificar os servidores de destino de um trabalho
Este tópico descreve como alterar os servidou oes de destino para trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para modificar os servidores de destino de um trabalho usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Por padrão, os membros da função de servidor fixa sysadmin podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do SQL Server Agent no banco de dados msdb:  
  
1.  **SQLAgentUserRole**  
  
2.  **SQLAgentReaderRole**  
  
3.  SQLAgentOperatorRole  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>Para modificar os servidores de destino de um trabalho  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse em um trabalho e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , selecione a página **Destinos**e clique em **Servidor local de destino**ou **Vários servidores de destino**.  
  
    Se optar por **Vários servidores de destino**, designe os servidores a serem destino do trabalho, marcando a caixa à esquerda do nome do servidor. Verifique se as caixas de seleção dos servidores que não devem ser destino do trabalho estão desmarcadas.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>Para modificar os servidores de destino de um trabalho  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo atribui o trabalho multisservidor Backups de Vendas Semanais ao servidor SEATTLE2.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
```  
  
Para obter mais informações, consulte [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286).  
  
## <a name="see-also"></a>Consulte também  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  

