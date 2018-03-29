---
title: Definir opções de etapa de trabalho Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb941b886668e3a1ab263979df51209815fd7c73
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como definir opções para etapas de trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent [!INCLUDE[tsql](../../includes/tsql_md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou SQL Server Management Objects.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para definir opções de etapa de trabalho Transact-SQL, usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-define-transact-sql-job-step-options"></a>Para definir opções de etapa de trabalho Transact-SQL  
  
1.  No **Pesquisador de Objetos**, expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e clique em **Propriedades**.  
  
2.  Clique na página **Etapas** , clique em uma etapa de trabalho e em **Editar**.  
  
3.  Na caixa de diálogo **Propriedades da Etapa de Trabalho** , confirme que o tipo de trabalho é **Script Transact-SQL (TSQL)**e selecione a página **Avançado** .  
  
4.  Especifique uma ação a tomar em caso de êxito do trabalho, dentre as opções da lista **Ação ao obter êxito** .  
  
5.  Especifique um número de tentativas, inserindo um número entre 0 e 9999 na caixa **Tentativas de repetição** .  
  
6.  Especifique um intervalo entre as tentativas, inserindo um número de minutos entre 0 e 9999 na caixa **Intervalo de repetição** .  
  
7.  Especifique uma ação a tomar em caso de falha do trabalho, dentre as opções da lista **Ação ao falhar** .  
  
8.  Se o trabalho for um script [!INCLUDE[tsql](../../includes/tsql_md.md)] , você poderá escolher entre as seguintes opções:  
  
    -   Inserir o nome de um **Arquivo de saída**. Por padrão, o arquivo é substituído sempre que a etapa de trabalho é executada. Se não quiser que o arquivo de saída seja substituído, marque **Anexar saída ao arquivo existente**. Essa opção só está disponível para membros da função de servidor fixa **sysadmin** . Observe que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] não permite aos usuários visualizar arquivos arbitrários no sistema de arquivos e, portanto, não é possível usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] para exibir logs de etapas de trabalho que são gravados no sistema de arquivos.  
  
    -   Marque **Registrar na tabela** , se desejar registrar a etapa de trabalho em uma tabela de banco de dados. Por padrão, o conteúdo da tabela é substituído sempre que a etapa de trabalho é executada. Se não quiser que o conteúdo da tabela seja substituído, marque **Anexar saída à entrada existente na tabela**. Após a execução da etapa de trabalho, o conteúdo dessa tabela pode ser visualizado clicando-se em **Exibir**.  
  
    -   Marque **Incluir saída da etapa no histórico** , se desejar que a saída seja incluída no histórico da etapa. A saída será exibida apenas se não houver erros. A saída também pode ser truncada.  
  
9. Se você for membro da função de servidor fixa **sysadmin** e desejar executar a etapa de trabalho como um logon SQL diferente, selecione esse logon na lista **Executar como usuário** .  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para definir opções de etapa de trabalho Transact-SQL**  
  
Use a classe **JobStep** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell.  
  
