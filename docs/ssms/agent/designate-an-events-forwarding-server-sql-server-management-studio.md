---
title: Designar um servidor de encaminhamento de eventos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d05b8e386a3df5314433dbf505e3c7682740434c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749050"
---
# <a name="designate-an-events-forwarding-server"></a>Designar um servidor de encaminhamento de eventos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como designar um servidor no qual o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encaminha eventos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Observe que o encaminhamento de eventos se aplica a eventos encaminhados entre servidores, não a eventos encaminhados entre instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedadas em um único computador. Note também que, para receber eventos encaminhados, o servidor de gerenciamento de alertas deve ser uma instância padrão do SQL Server.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Para designar um servidor de encaminhamento de eventos  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor do qual você deseja encaminhar eventos para outro servidor.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent –** _nome_do_servidor_, em **Selecionar uma página**, selecione **Avançado**.  
  
4.  Em **Encaminhamento de evento do SQL Server**, marque a caixa de seleção **Encaminhar eventos para um servidor diferente** .  
  
5.  Na lista **Servidor** , selecione um servidor e, em **Eventos**, selecione um destes procedimentos:  
  
    -   Selecione **Eventos sem tratamento** para encaminhar apenas os eventos que não foram manipulados por alertas locais.  
  
    -   Selecione **Todos os eventos** para encaminhar todos os eventos, independentemente de terem sido manipulados por alertas locais.  
  
6.  Na lista **Se a severidade do evento for esta ou acima** , clique no nível de severidade em que os eventos devem ser encaminhados para o servidor selecionado.  
  
7.  Quando terminar, clique em **OK**.  
  
