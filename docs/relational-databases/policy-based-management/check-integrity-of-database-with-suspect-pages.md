---
title: Verificar a integridade do banco de dados com páginas suspeitas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34fa55b53fac6b214480d0bed2b8224bcebeb7d1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="check-integrity-of-database-with-suspect-pages"></a>Verificar a integridade do banco de dados com páginas suspeitas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica os bancos de dados de usuários que têm o status do banco de dados definido como suspeito. Quando o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] lê uma página do banco de dados que contém um erro 824, a página é considerada suspeita, sua ID é registrada na tabela suspect_pages do msdb e o banco de dados que a contém é definido como suspeito.  
  
 O erro 824 indica que um erro de consistência lógico foi detectado durante uma operação de leitura. Esse erro frequentemente indica a corrupção de dados causada por um componente de subsistema de E/S defeituoso. Este é um erro grave que ameaça a integridade do banco de dados e deve ser corrigido imediatamente.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
  
-   Revise o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter os detalhes do erro 824 para esse banco de dados.  
  
-   Execute uma verificação de consistência completa do banco de dados ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)).  
  
-   Implemente as ações de usuário definidas em [MSSQLSERVER_824](http://go.microsoft.com/fwlink/?LinkId=81397).  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
