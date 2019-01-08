---
title: Alterar o tempo de recuperação de destino de um banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 36be65b9e359d4fe115e2b410db181f049c1eccd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766818"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>Alterar o tempo de recuperação de destino de um banco de dados (SQL Server)
  Este tópico descreve como definir o tempo de recuperação de destino de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por padrão, o tempo de recuperação de destino é 0, e o banco de dados usa *pontos de verificação automáticos* (que são controlados pela opção de servidor **intervalo de recuperação** ). Definir o tempo de recuperação de destino como maior que 0 faz com que o banco de dados use os *pontos de verificação indiretos* e estabelece um limite superior no tempo de recuperação para este banco de dados.  
  
> [!NOTE]  
>  O limite superior especificado para um determinado banco de dados pela sua configuração de tempo de recuperação de destino poderá ser excedido se uma transação de longa execução provocar tempos excessivos de UNDO.  
  
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [segurança](#Security)  
  
-   **Para alterar a recuperação de destino de tempo, usando:**  [SQL Server Management Studio](#SSMSProcedure) ou [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a>  
  
> [!CAUTION]  
>  Uma carga de trabalho transacional online em um banco de dados configurado para pontos de verificação indiretos pode apresentar degradação no desempenho. Pontos de verificação indiretos garantem que o número de páginas sujas esteja abaixo de certo limite, para que a recuperação do banco de dados seja concluída dentro da meta do tempo de recuperação. A opção de configuração do intervalo de recuperação usa o número de transações para determinar o tempo de recuperação em relação aos pontos de verificação indiretos, que usam o número de páginas sujas. Quando pontos de verificação indiretos são habilitados em um banco de dados que recebe um grande número de operações DML, o gravador em segundo plano pode iniciar eliminação agressiva de buffers sujos no disco para garantir que o tempo necessário para executar a recuperação esteja dentro da meta do tempo de recuperação definido para o banco de dados. Isso pode causar atividade adicional de E/S em determinados sistemas, o que pode contribuir para um gargalo de desempenho, se o subsistema do disco estiver operando acima ou próximo do limite de E/S.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para alterar o tempo de recuperação de destino**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Clique com o botão direito do mouse no banco de dados a ser alterado e clique no comando **Propriedades** .  
  
3.  Na caixa de diálogo **Propriedades do Banco de Dados** , clique na página **Opções** .  
  
4.  No painel **Recuperação** , no campo **Tempo de Recuperação de Destino (Segundos)** , especifique o número de segundos desejado como o limite superior do tempo de recuperação deste banco de dados.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para alterar o tempo de recuperação de destino**  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o banco de dados reside.  
  
2.  Use a instrução [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options), da seguinte maneira:  
  
     TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     Quando maior que 0 (o padrão), especifica o limite superior do tempo de recuperação para o banco de dados especificado no caso de uma falha.  
  
     SECONDS  
     Indica que *target_recovery_time* é expresso como o número de segundos.  
  
     MINUTES  
     Indica que *target_recovery_time* é expresso como o número de minutos.  
  
     O exemplo a seguir define o tempo de recuperação de destino do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como `60` segundos.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
