---
title: Definir o desligamento da execução de trabalhos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 283768ef7189335965e942ecd8e6810cc9d981e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842984"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como definir o tempo que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve esperar pelo término dos trabalhos em execução antes de encerrar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para definir um tempo de desligamento para um trabalho do SQL Server Agent, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Por padrão, os membros da função de servidor fixa **sysadmin** podem marcar a hora que o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esperará para executar trabalhos para concluir antes de o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent finalizá-los. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>Para definir desligamento de execução de trabalho  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor no qual você deseja definir um intervalo de desligamento de execução de trabalho.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Em **Selecione uma página**, selecione **Sistema de Trabalho**.  
  
4.  Defina o **Intervalo de tempo limite de desligamento** em segundos para aumentar ou diminuir o intervalo do tempo limite para o desligamento. Isso determina quanto tempo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent aguardará pelo término dos trabalhos em execução antes de o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent terminar.  
  
