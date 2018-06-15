---
title: Manipular várias etapas de trabalho | Microsoft Docs
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
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3b88a2d50bd748da3e56d43367706715fa4739f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33043863"
---
# <a name="handle-multiple-job-steps"></a>Manipular várias etapas de trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Se um trabalho tiver mais de uma etapa, você terá que especificar a ordem em que as etapas de trabalho devem ser executadas. Isso é chamado *controle de fluxo**.* Você pode adicionar novas etapas de trabalho e reorganizar o fluxo a qualquer hora; as alterações entram em vigor na próxima vez em que o trabalho é executado. Essa ilustração mostra o controle de fluxo para um trabalho de backup de banco de dados.  
  
![Controle de fluxo de etapas de trabalho do SQL Server Agent](../../ssms/agent/media/dbflow01.gif "Controle de fluxo de etapas de trabalho do SQL Server Agent")  
  
A primeira etapa é Fazer Backup do Banco de Dados. Se essa etapa falhar, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent informará a falha ao operador definido para receber a notificação. Se a etapa Fazer Backup de Banco de Dados tiver êxito, o trabalho passará à próxima etapa, “Scrub” dos Dados do Cliente. Se essa etapa falhar, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent irá passar para a etapa Recuperar Banco de Dados. Se "Scrub" dos Dados do Cliente tiver êxito, o trabalho passará à próxima etapa, Atualizar Estatísticas e assim por diante, até que a etapa final resulte em Informar Êxito ou Informar Falha.  
  
É você quem define a ação de controle de fluxo quanto ao êxito ou falha de cada etapa do trabalho. É preciso especificar a ação a ser tomada mediante o êxito ou a falha da etapa de trabalho. Você também pode definir o número de novas tentativas, em caso de falha da etapa de trabalho e o intervalo entre elas.  
  
> [!NOTE]  
> Quando a GUI do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é utilizada para excluir uma ou mais etapas de um trabalho com várias etapas, ela remove todas as etapas e, em seguida, adiciona novamente as etapas restantes com as referências corretas das ações em caso de êxito ou falha. Por exemplo, suponha que você tenha um trabalho com cinco etapas e que a primeira etapa esteja configurada para passar à etapa 4, caso obtenha êxito. Se você excluir a etapa 3, a GUI removerá todas as etapas do trabalho e adicionará as quatro etapas restantes (1, 2, 4 e 5) com as referências corretas. Nesse caso, a referência na etapa 1 seria reconfigurada para passar à etapa 3, caso a etapa 1 obtenha êxito.  
  
As etapas de trabalho devem ser autossuficientes. Ou seja, um trabalho não pode transmitir valores Boolianos, dados ou valores numéricos entre etapas de trabalho. É possível, contudo, transmitir valores de uma etapa de trabalho [!INCLUDE[tsql](../../includes/tsql_md.md)] para outra, usando tabelas permanentes ou tabelas temporárias globais. É possível transmitir valores entre etapas de trabalho que executam programas executáveis, de uma etapa de trabalho para outra usando arquivos. Por exemplo, o executável de uma etapa de trabalho grava um arquivo e o executável da etapa subsequente o lê.  
  
> [!NOTE]  
> Se você criar etapas de trabalho em loop (etapa 1 seguida da etapa 2, então a etapa 2 retorna à etapa 1), aparecerá uma mensagem de aviso quando o trabalho for criado pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent registra as informações do trabalho e suas etapas no histórico de trabalhos.  
  
## <a name="see-also"></a>Consulte Também  
[sp_add_job](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
[sysjobs (Transact-SQL)](http://msdn.microsoft.com/en-us/e244a6a5-54c2-47a6-8039-dd1852b0ae59)  
[sysjobsteps](http://msdn.microsoft.com/en-us/978b8205-535b-461c-91f3-af9b08eca467)  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)  
  
