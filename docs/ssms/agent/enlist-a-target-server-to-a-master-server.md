---
description: Inscrever um servidor de destino em um servidor mestre
title: Inscrever um servidor de destino em um servidor mestre
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 63798bf4c5697adabfce39317883792ff73de2c6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97423847"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Inscrever um servidor de destino em um servidor mestre
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Este tópico descreve como adicionar servidores de destino a uma configuração de administração multisservidor. Execute este procedimento a partir do servidor mestre. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SMO (SQL Server Management Objects).  
  
Para obter informações sobre como a conta do Windows usada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent afeta um ambiente multisservidor, consulte [Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
A criptografia TLS (protocolo TLS) completa, anteriormente conhecida como SSL (protocolo SSL), e a validação de certificado são habilitadas para conexões entre servidores mestres e servidores de destino por padrão. Para obter mais informações, veja [Definir opções de criptografia em servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Para inscrever um servidor de destino  
  
1.  No **Pesquisador de Objetos**, expanda um servidor que esteja configurado como servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor** e clique em **Adicionar Servidores de Destino**.  
  
3.  Complete o Assistente de Servidor de Destino, que o guia nesse processo.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Para inscrever um servidor de destino  
  
1.  Use o procedimento armazenado **sp_msx_enlist** .  Para obter mais informações, veja [sp_msx_enlist (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
