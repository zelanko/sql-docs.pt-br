---
title: Fazer backup e restaurar bancos de dados do sistema (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 51ccf1aeadcf4ab9a662cdd629a812d3ee4b82aa
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959746"
---
# <a name="back-up-and-restore-of-system-databases-sql-server"></a>Fazer backup e restaurar bancos de dados do sistema (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém um conjunto de bancos de dados em nível de sistema,*bancos de dados do sistema*, essenciais para a operação de uma instância do servidor. Deve ser feito backup de vários bancos de dados do sistema após cada atualização significativa. Os bancos de dados do sistema que você sempre deve fazer backup incluem **msdb**, **mestre**e **modelo**. Se qualquer banco de dados usar replicação na instância de servidor, haverá um banco de dados do sistema de **distribuição** do qual também deverá ser feito backup. Os backups desses bancos de dados do sistema permitem que você restaure e recupere o sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no caso de falha do sistema, como a perda de um disco rígido.  
  
 A tabela a seguir resume todos os bancos de dados do sistema.  
  
|Banco de dados do sistema|Descrição|Requer backups?|modelo de recuperação|Comentários|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[mestre](../databases/master-database.md)|O banco de dados que registra todas as informações de nível de sistema para um sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Sim|Simples|Faça backup do **mestre** com a frequência necessária para proteger adequadamente os dados para suas necessidades empresariais. Recomendamos uma agenda regular de backup, que você pode complementar com um backup adicional após uma atualização significativa.|  
|[modelo](../databases/model-database.md)|O modelo de todos os bancos de dados criados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sim|Configurável pelo usuário<sup>1</sup>|Faça backup do **modelo** somente quando necessário para suas necessidades empresariais; por exemplo, logo após personalizar suas opções de banco de dados.<br /><br /> **Prática recomendada:** é recomendável criar somente backups completos de bancos de dados do **modelo**, conforme necessário. Como **model** é pequeno e raramente alterado, é desnecessário fazer backup do log.|  
|[msdb](../databases/msdb-database.md)|O banco de dados é usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para programar alertas e trabalhos, e também para registrar operadores. O**msdb** também contém tabelas de histórico, como as tabelas de histórico de backup e de restauração.|Sim|Simples (padrão)|Faça backup do **msdb** sempre que este for atualizado.|  
|[Resource](../databases/resource-database.md) (RDB)|Um banco de dados somente leitura que contém cópias de todos os objetos do sistema fornecido com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Não|-|O banco de dados **Resource** reside no arquivo mssqlsystemresource.mdf, que contém somente código. Portanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode fazer backup do banco de dados **Recurso** .<br /><br /> Observação: Você pode executar um backup baseado em arquivo ou disco no arquivo mssqlsystemresource.mdf tratando o arquivo como se fosse um arquivo binário (.exe) em vez de um arquivo de banco de dados. Mas você não pode usar a restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos backups. A restauração de uma cópia de backup de mssqlsystemresource.mdf pode ser feita apenas manualmente, e é necessário ter cuidado para não substituir o banco de dados **Resource** atual com uma versão desatualizada ou potencialmente insegura.|  
|[tempdb](../databases/tempdb-database.md)|Um workspace para manter conjuntos de resultados temporários ou intermediários. Esse banco de dados é recriado sempre que é iniciada uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando a instância de servidor é desativada, qualquer dado em **tempdb** é excluído permanentemente.|Não|Simples|Você não poderá fazer backup do banco de dados do sistema **tempdb** .|  
|[Configurar Distribuição](../replication/configure-distribution.md)|Um banco de dados que existe somente se o servidor estiver configurado como um Distribuidor de replicação. Esse banco de dados armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional.|Sim|Simples|Para obter informações sobre quando fazer backup do banco de dados **distribution** , veja [Fazer backup e restaurar bancos de dados replicados](../replication/administration/back-up-and-restore-replicated-databases.md).|  
  
 <sup>1</sup> para aprender o modelo de recuperação atual do modelo, consulte [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md) ou [sys. databases &#40;&#41;do Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
## <a name="limitations-on-restoring-system-databases"></a>Limitações da restauração de bancos de dados do sistema  
  
-   Os bancos de dados do sistema podem ser restaurados somente a partir de backups criados na versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está em execução na instância de servidor no momento. Por exemplo, para restaurar um banco de dados do sistema em uma instância de servidor em execução no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1.  
  
-   Para restaurar qualquer banco de dados, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar em execução. Iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que o banco de dados **mestre** esteja acessível e pelo menos parcialmente utilizável. Se o **mestre** se tornar inutilizável, você poderá retornar o banco de dados a um estado utilizável das seguintes maneiras:  
  
    -   Restaure o **mestre** a partir de um backup de banco de dados atual.  
  
         Se você puder iniciar a instância de servidor, deverá poder restaurar o **mestre** a partir de um backup de banco de dados completo.  
  
    -   Recrie completamente o **mestre** .  
  
         Se danos graves do **master** impedirem a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recrie o **master**. Para obter mais informações, consulte [Recriar bancos de dados do sistema](../databases/system-databases.md).  
  
        > [!IMPORTANT]  
        >  A recriação de **master** recria todos os bancos de dados do sistema.  
  
-   Em algumas circunstâncias, os problemas que recuperam o banco de dados modelo podem exigir a reconstrução dos bancos de dados do sistema ou a substituição dos arquivos mdf e ldf para o banco de dados modelo. Para obter mais informações, consulte [Recriar bancos de dados do sistema](../databases/system-databases.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](complete-database-restores-simple-recovery-model.md)  
  
-   [Restaurar o banco de dados mestre &#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  
-   [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [Mover bancos de dados do sistema](../databases/move-system-databases.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Banco de dados de distribuição](../../relational-databases/replication/distribution-database.md)   
 [Banco de dados mestre](../databases/master-database.md)   
 [Banco de dados msdb](../databases/msdb-database.md)   
 [Banco de dados modelo](../databases/model-database.md)   
 [Banco de dados de recursos](../databases/resource-database.md)   
 [Banco de dados tempdb](../databases/tempdb-database.md)  
  
  
