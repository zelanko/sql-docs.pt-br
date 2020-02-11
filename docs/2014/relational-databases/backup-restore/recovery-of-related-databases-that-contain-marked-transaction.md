---
title: Recuperação de bancos de dados relacionados que contêm uma transação marcada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 209bc81c63998cea299d2c377175955ee99470c4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62875718"
---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>Recuperação de bancos de dados relacionados que contêm transação marcada
  Este tópico é relevante apenas para os bancos de dados que contêm transações marcadas e que usam modelos de recuperação bulk-logged ou completos.  
  
 Para obter informações sobre os requisitos de restauração para um ponto de recuperação específico, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à inserção de marcas nomeadas no log de transações, permitindo a recuperação nessa marca específica. As marcas de log são transações específicas e são inseridas apenas se as suas transações associadas forem confirmadas. Desse modo, as marcas podem ser ligadas ao trabalho específico e você pode recuperá-las em um ponto que inclua ou exclua esse trabalho.  
  
 Antes de você inserir marcas nomeadas no log de transações, considere o seguinte:  
  
-   Como as marcas de transação consomem espaço de log, só as use para transações que têm um papel significativo na estratégia de recuperação de banco de dados.  
  
-   Depois que a transação marcada é confirmada, uma linha é inserida na tabela [logmarkhistory](/sql/relational-databases/system-tables/logmarkhistory-transact-sql) no **msdb**.  
  
-   Se uma transação marcada abrange vários bancos de dados no mesmo servidor de banco de dados ou em servidores diferentes, as marcas devem ser registradas nos logs de todos os bancos de dados afetados. Para obter mais informações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
> [!NOTE]  
>  Para obter informações sobre como marcar transações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>Sintaxe Transact-SQL para inserir marcas nomeadas em um log de transações  
 Para inserir marcas nos logs de transações, use a instrução [BEGIN TRANSACTION](/sql/t-sql/language-elements/begin-transaction-transact-sql) e a cláusula WITH MARK [*descrição*]. A marca é nomeada igual à transação. A *descrição* opcional é uma descrição textual da marca, não o nome da marca. Por exemplo, o nome da transação e da marca criado na seguinte instrução `BEGIN TRANSACTION` é `Tx1`:  
  
```wmimof  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 O log de transações registra o nome da marca (nome da transação), descrição, banco de dados, usuário, informações `datetime` e o LSN (Log Sequence Number). As informações `datetime` são usadas com o nome da marca exclusivamente para identificar a marca.  
  
 Para obter informações sobre como inserir uma marca em uma transação que abrange vários bancos de dados, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>Sintaxe Transact-SQL para recuperar a uma marca  
 Quando você assinala uma transação marcada usando uma instrução[RESTORE LOG](/sql/t-sql/statements/restore-statements-transact-sql), é possível usar uma das seguintes cláusulas para parar na marca ou imediatamente antes dela:  
  
-   Use a cláusula WITH STOPATMARK **=*`<mark_name>`*' '** para especificar que a transação marcada é o ponto de recuperação.  
  
     O STOPATMARK roll-forward até a marca e inclui a transação marcada no roll-forward.  
  
-   Use a cláusula WITH STOPBEFOREMARK **=*`<mark_name>`*' '** para especificar que o registro de log que está imediatamente antes da marca é o ponto de recuperação.  
  
     O STOPATMARK roll-forward até a marca e exclui a transação marcada do roll-forward.  
  
 Ambas as opções STOPATMARK e STOPBEFOREMARK dão suporte a uma cláusula opcional AFTER *datetime* . Quando *datetime* é usado, os nomes da marca não precisam ser exclusivos.  
  
 Se AFTER *datetime* for omitido, o roll forward será interrompido na primeira marca que tem o nome especificado. Se AFTER *datetime* for especificado, o roll forward será interrompido na primeira marca que tem o nome especificado, exatamente em *datetime*ou após ele.  
  
> [!NOTE]  
>  Como em todas as operações de restauração point-in-time, não é permitido recuperar a uma marca quando o banco de dados estiver passando por operações com log de operações em massa.  
  
 **Para restaurar a uma transação marcada**  
  
 [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
### <a name="preparing-the-log-backups"></a>Preparando os backups de log  
 Para este exemplo, uma estratégia de backup apropriada para estes bancos de dados relacionados seria a seguinte:  
  
1.  Use o modelo de recuperação completa para ambos os bancos de dados.  
  
2.  Crie um backup completo de cada banco de dados.  
  
     Os backups dos bancos de dados podem ser feitos consecutivamente ou simultaneamente.  
  
3.  Antes de fazer o backup do log de transações, marque uma transação que execute em todos os bancos de dados. Para obter informações sobre como criar as transações marcadas, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
4.  Faça o backup do log de transações em cada banco de dados.  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>Recuperando um banco de dados a uma transação marcada  
 **Para restaurar o backup**  
  
1.  Crie [backups da parte final do log](tail-log-backups-sql-server.md) dos bancos de dados não danificados, se possível.  
  
2.  Restaure o backup completo mais recente do banco de dados de cada banco de dados.  
  
3.  Identifique a transação marcada mais recente disponível em todos os backups de log de transações. Essa informação é armazenada na tabela **logmarkhistory** no banco de dados **msdb** em cada servidor.  
  
4.  Identifique os backups de log para todos os bancos de dados relacionados que contêm essa marca.  
  
5.  Restaure cada backup de log, parando na transação marcada.  
  
6.  Recupere cada banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Planejar e executar sequências de restauração &#40;Modelo de recuperação completa&#41;](plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
