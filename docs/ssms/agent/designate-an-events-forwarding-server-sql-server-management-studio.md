---
title: Designar um servidor de encaminhamento de eventos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7995d03fa1c20b79197b941f9235890759ee941c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como designar um servidor para o qual o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] encaminhe eventos no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] . Observe que o encaminhamento de eventos se aplica a eventos encaminhados entre servidores, não a eventos encaminhados entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] hospedadas em um único computador. Note também que, para receber eventos encaminhados, o servidor de gerenciamento de alertas deve ser uma instância padrão do SQL Server.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para designar um servidor de encaminhamento de eventos, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Para designar um servidor de encaminhamento de eventos  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor do qual você deseja encaminhar eventos para outro servidor.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent –***server_name*, em **Selecionar uma página**, selecione **Avançado**.  
  
4.  Em **Encaminhamento de evento do SQL Server**, marque a caixa de seleção **Encaminhar eventos para um servidor diferente** .  
  
5.  Na lista **Servidor** , selecione um servidor e, em **Eventos**, selecione um destes procedimentos:  
  
    -   Selecione **Eventos sem tratamento** para encaminhar apenas os eventos que não foram manipulados por alertas locais.  
  
    -   Selecione **Todos os eventos** para encaminhar todos os eventos, independentemente de terem sido manipulados por alertas locais.  
  
6.  Na lista **Se a severidade do evento for esta ou acima** , clique no nível de severidade em que os eventos devem ser encaminhados para o servidor selecionado.  
  
7.  Quando terminar, clique em **OK**.  
  
