---
description: Propriedades do SQL Server Agent (página Geral)
title: Propriedades do SQL Server Agent (página Geral)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f08f8fe21876f5a04e817c367ece49d44eef93c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88370912"
---
# <a name="sql-server-agent-properties-general-page"></a>Propriedades do SQL Server Agent (página Geral)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Use esta página para exibir e modificar as propriedades gerais do serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Estado do serviço**  
Exibe o estado atual do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Reiniciar automaticamente o SQL Server se ele parar inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent reiniciará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parar inesperadamente.  
  
**Reiniciar automaticamente o SQL Server Agent se ele parar inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reiniciará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent parar inesperadamente.  
  
**Filename**  
Especifica o nome do arquivo para o log de erros.  
  
**...**  
Navegue até o arquivo de log de erros.  
  
**Incluir mensagens de rastreamento de execução**  
Inclui mensagens de rastreamento de execução no log de erros. As mensagens de rastreamento fornecem informações detalhadas sobre a operação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Portanto, o arquivo de log requer mais espaço em disco quando essa opção é selecionada. Essa opção só deve ser selecionada ao solucionar um problema que possa envolver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Gravar arquivo OEM**  
Grava o arquivo de log de erros como um arquivo não Unicode. Isso reduz a quantidade de espaço em disco consumida pelo arquivo de log. Porém, mensagens que incluem dados Unicode podem ser mais difíceis de ler quando essa opção é habilitada.  
  
**Destinatário do net send**  
Digite o nome de um operador para receber a notificação net send das mensagens que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent gravar no arquivo de log.  
  
## <a name="see-also"></a>Consulte Também  
[Operadores](../../ssms/agent/operators.md)  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
