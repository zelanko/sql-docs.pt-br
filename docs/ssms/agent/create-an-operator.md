---
title: Criar um operador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3148f0193fab0c760d3c8a1a169e0ba2c4a2c009
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42775000"
---
# <a name="create-an-operator"></a>Create an Operator
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como configurar um usuário para receber notificações sobre trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para criar um operador usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   As opções Pager e **net send** serão removidas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses recursos em novo trabalho de desenvolvimento e planeje modificar os aplicativos que os usam atualmente.  
  
-   Observe que o SQL Server Agent deve ser configurado para usar o Database Mail a fim de enviar notificações por pager ou email a operadores. Para obter mais informações, consulte [Atribuir alertas a um operador](assign-alerts-to-an-operator.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Somente membros da função de servidor fixa **sysadmin** podem criar operadores.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>Para criar um operador  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar o operador do SQL Server Agent.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Operadores** e selecione **Novo Operador**.  
  
    As opções a seguir estão disponíveis na página **Geral** da caixa de diálogo **Novo Operador** :  
  
    **Nome**  
    Altera o nome do operador.  
  
    **Habilitado**  
    Habilita o operador. Quando não estiver habilitado, nenhuma notificação será enviada ao operador.  
  
    **Nome de email**  
    Especifica o endereço de email do operador.  
  
    **Endereço de net send**  
    Especifique o endereço a ser usado para **net send**.  
  
    **Nome de e-mail de pager**  
    Especifica o endereço de email a ser usado para o pager do operador.  
  
    **Agenda em serviço do pager**  
    Marca as horas em que o pager está ativo.  
  
    **Segunda-feira - Domingo**  
    Selecione os dias em que o pager está ativo.  
  
    **Início do dia útil**  
    Selecione a hora do dia depois da qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent envia mensagens ao pager.  
  
    **Término do dia útil**  
    Selecione a hora do dia depois da qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para de enviar mensagens ao pager.  
  
    As opções a seguir estão disponíveis na página **Notificações** da caixa de diálogo **Novo Operador** :  
  
    **Alertas**  
    Exiba os alertas na instância.  
  
    **Trabalhos**  
    Exiba os trabalhos na instância.  
  
    **Lista de alertas**  
    Lista os alertas na instância.  
  
    **Lista de trabalhos**  
    Lista os trabalhos na instância.  
  
    **Email**  
    Notifique este operador por email.  
  
    **Pager**  
    Notifique este operador enviando e-mail ao endereço de pager.  
  
    **Net send**  
    Notifique este operador pelo **net send**.  
  
4.  Quando terminar de criar o novo operador, clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-create-an-operator"></a>Para criar um operador  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- sets up the operator information for user 'danwi.'
    -- The operator is enabled.   
    -- SQL Server Agent sends notifications by pager 
    -- from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_add_operator (Transact-SQL)](http://msdn.microsoft.com/817cd98a-4dff-4ed8-a546-f336c144d1e0).  
  
