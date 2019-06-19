---
title: Servidores de destino (guia Status do Servidor de Destino) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.target.status.f1
ms.assetid: 010a4cab-d878-4889-8ac8-7d91db6345d6
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3e40e3615932b0ff1615760d851d118173faa559
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65097515"
---
# <a name="target-servers-target-server-status-tab"></a>Servidores de Destino (Guia do Status do Servidor de Destino)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir o status dos servidores de destino para esse servidor mestre.  
  
## <a name="options"></a>Opções  
**Servidor de Destino**  
Exiba o nome do servidor de destino.  
  
**Hora local**  
Exiba a data e hora do servidor de destino no fuso horário local para aquele servidor.  
  
**Última sondagem**  
Exiba a data e hora local em que o servidor de destino fez a última sondagem do mestre.  
  
**Instruções não lidas**  
Exiba o número de instruções que o servidor de destino ainda não recebeu.  
  
**Status**  
Exiba o status do servidor de destino.  
  
**Forçar Sondagem**  
Clique nesse botão para forçar os servidores de destino selecionados a executar sondagem do servidor mestre.  
  
**Forçar Remoção**  
Clique nesse botão para forçar os servidores de destino selecionados a remover o servidor mestre.  
  
**Postar Instruções**  
Poste instruções para os servidores de destino selecionados.  
  
**Habilitar Atualização Automática**  
Selecione essa opção para atualizar automaticamente a informações exibida.  
  
**Atualizar a cada**  
Especifique com que frequência as informações nessa página são atualizadas.  
  
## <a name="see-also"></a>Consulte Também  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
