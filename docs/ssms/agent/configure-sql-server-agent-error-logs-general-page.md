---
description: Configurar Logs de Erros do SQL Server Agent (página Geral)
title: Configurar logs de erros (página Geral)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 85ae0e4833a1f17f2bd4a795886be8453d61bafd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482239"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>Configurar Logs de Erros do SQL Server Agent (página Geral)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Use esta tela para exibir e atualizar as configurações de log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Arquivo de log de erros**  
Especifica o arquivo em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent grava logs de erros.  
  
**...**  
Navegue até o arquivo de log de erros.  
  
**Gravar log de erros OEM**  
Grava o arquivo de log de erros como um arquivo não Unicode. Isso reduz a quantidade de espaço em disco consumida pelo arquivo de log. Porém, mensagens que incluem dados Unicode podem ser mais difíceis de ler quando essa opção é habilitada.  
  
**Erros**  
Só grava erros e mensagens informativas no arquivo de log.  
  
**Warnings**  
Só grava avisos e mensagens informativas no arquivo de log.  
  
**Informações**  
Só grava mensagens informativas no arquivo de log.  
  
## <a name="see-also"></a>Consulte Também  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
