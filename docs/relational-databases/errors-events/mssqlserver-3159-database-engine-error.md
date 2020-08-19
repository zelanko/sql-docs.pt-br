---
description: MSSQLSERVER_3159
title: MSSQLSERVER_3159 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3159 (Database Engine error)
ms.assetid: c93c1003-0e3a-40aa-9873-44a0f5b8b57e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f2ad1730a79f7dfeed6972fc92a084a6a28e2166
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424308"
---
# <a name="mssqlserver_3159"></a>MSSQLSERVER_3159
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3159|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_LOGNOTBACKEDUP|  
|Texto da mensagem|Não foi feito backup da parte final do log do banco de dados "%ls". Use BACKUP LOG WITH NORECOVERY para fazer backup do log se ele contiver um trabalho que você não deseja perder. Use a cláusula WITH REPLACE ou WITH STOPAT da instrução RESTORE para simplesmente substituir o conteúdo do log.|  
  
## <a name="explanation"></a>Explicação  
Na maioria dos casos, sob os modelos de recuperação bulk-logged ou de operações em massa, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que você faça backup do final do log para capturar os registros de log que ainda não sofreram backup. Um backup de log realizado no final do log imediatamente antes de uma operação de restauração é chamado de backup de final do log.  
  
Quando você estiver recuperando um banco de dados até o ponto de uma falha, o backup do final do log é o último backup de interesse no plano de recuperação. Se você não puder fazer backup da parte final do log, apenas será possível recuperar um banco de dados até o fim do último backup criado antes da falha.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente requer que você faça um backup do final do log antes de começar a restaurar um banco de dados. O backup da parte final do log impede perda de trabalho e mantém a cadeia de logs intacta. Porém, nem todos os cenários de restauração requerem um backup de final do log. Você não precisará ter um backup do final do log se o ponto de recuperação estiver incluído em um backup de log anterior, ou se estiver movendo ou substituindo o banco de dados e não precisar restaurá-lo em um momento determinado após o backup mais recente. Além disso, se os arquivos de log estiverem danificados e não for possível criar um backup da parte final do log, você deverá restaurar o banco de dados sem usar um backup da parte final do log. Todas as transações confirmadas depois do último backup de log são perdidas. Para obter mais informações, consulte "Restaurando sem usar um backup de final do log", adiante neste tópico.  
  
> [!CAUTION]  
> REPLACE raramente deve ser usado, e só depois de consideração cuidadosa.  
  
## <a name="user-action"></a>Ação do usuário  
Faça um backup de final do log e tente novamente a operação de restauração.  
  
Se você não puder fazer um backup de final do log, use WITH STOPAT ou WITH REPLACE em suas instruções RESTORE.  
  
## <a name="see-also"></a>Consulte Também  
[Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](~/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
[Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
[Fazer backup de um log de transações &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
[Backups da parte final do log &#40;SQL Server&#41;](~/relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
