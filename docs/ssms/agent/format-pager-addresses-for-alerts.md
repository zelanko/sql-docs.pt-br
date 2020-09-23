---
description: Format Pager Addresses for Alerts
title: Format Pager Addresses for Alerts
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8c75d7eaf25941969ddbf9e9d9dfc2cb683c1360
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492187"
---
# <a name="format-pager-addresses-for-alerts"></a>Format Pager Addresses for Alerts
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Este tópico descreve como formatar endereços de pager para alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Por padrão, os membros da função de servidor fixa **sysadmin** podem exibir as informações sobre um alerta. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>Para formatar endereços de pager  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o alerta que você deseja excluir enviar para um pager.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**  
  
3.  Em **Selecione uma página**, selecione **Sistema de Alerta**.  
  
4.  Nas caixas **Linha Para** e **Linha Cc** do campo **Formatação de endereço para emails por pager** , insira o prefixo ou sufixo de endereço de pager. O endereço de pager atual do operador é inserido quando uma notificação é enviada.  
  
5.  Na caixa **Assunto** , insira o prefixo ou sufixo de linha de assunto.  
  
6.  Marque a caixa de seleção **Incluir corpo do email na página de notificação** para incluir a mensagem de email inteira na mensagem do pager (em vez de apenas a linha do assunto).  
  
7.  Quando terminar, clique em **OK**.  
  
