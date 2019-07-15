---
title: Propriedades do alerta – Novo alerta (página Opções) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3b38dd0998a4da2e3a4f207fe203ecd848bd9c4c
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67688999"
---
# <a name="alert-properties---new-alert-options-page"></a>Propriedades do alerta – Novo alerta (página Opções)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir e modificar opções para os alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  

## <a name="options"></a>Opções  
**Email**  
Inclua texto de erro do evento, se houver, em notificações de email.  
  
**Pager**  
Inclua texto de erro do evento, se houver, em notificações de pager.  
  
**Net send**  
Inclua texto de erro do evento, se houver, em notificações enviadas pela net.  
  
**Mensagem de notificação adicional para enviar**  
Digite qualquer texto adicional para incluir em mensagens de notificação.  
  
**Atraso entre as respostas**  
Especifique um intervalo para ocorrências repetidas do evento. Alguns eventos podem acontecer com frequência durante um curto intervalo de tempo. Nesse caso, você pode desejar saber que o evento ocorreu, mas talvez não queira uma resposta para cada evento. Use essa opção para especificar um tempo-limite. Com o intervalo, depois que o alerta responde a um evento, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent espera pelo intervalo especificado antes de responder novamente, mesmo se o evento ocorrer durante o intervalo.  
  
**Minutes (minutos) (minutos)**  
Especifique um intervalo em minutos. Para responder todas as vezes que o evento ocorrer, especifique 0 minuto e 0 segundo.  
  
**Seconds (segundos) (segundos)**  
Especifique um intervalo em segundos. Para responder todas as vezes que o evento ocorrer, especifique 0 minuto e 0 segundo.  
  
## <a name="see-also"></a>Consulte Também  
[Alertas](../../ssms/agent/alerts.md)  
  
