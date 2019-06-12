---
title: Alterar o tempo de recuperação de destino de um banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f47d33179fb382472def9950a928be137e1f6583
ms.sourcegitcommit: 36c5f28d9fc8d2ddd02deb237937c9968d971926
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354387"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>Alterar o tempo de recuperação de destino de um banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como definir o tempo de recuperação de destino de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por padrão, o tempo de recuperação de destino é de 60 segundos e o banco de dados usa *pontos de verificação indiretos*. O tempo de recuperação de destino estabelece um limite superior no tempo de recuperação deste banco de dados.  
  
> [!NOTE]  
>  O limite superior especificado para um determinado banco de dados pela sua configuração de tempo de recuperação de destino poderá ser excedido se uma transação de longa execução provocar tempos excessivos de UNDO.  
  
-   **Antes de começar:**  [Limitações e Restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para alterar o tempo de recuperação de destino usando:**  [SQL Server Management Studio](#SSMSProcedure) ou [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições 
  
> [!CAUTION]  
>  Uma carga de trabalho transacional online em um banco de dados configurado para pontos de verificação indiretos pode apresentar degradação no desempenho. Pontos de verificação indiretos garantem que o número de páginas sujas esteja abaixo de certo limite, para que a recuperação do banco de dados seja concluída dentro da meta do tempo de recuperação. A opção de configuração do intervalo de recuperação usa o número de transações para determinar o tempo de recuperação em relação aos pontos de verificação indiretos, que usam o número de páginas sujas. Quando pontos de verificação indiretos são habilitados em um banco de dados que recebe um grande número de operações DML, o gravador em segundo plano pode iniciar eliminação agressiva de buffers sujos no disco para garantir que o tempo necessário para executar a recuperação esteja dentro da meta do tempo de recuperação definido para o banco de dados. Isso poderá causar atividade adicional de E/S em determinados sistemas, o que pode contribuir para um gargalo de desempenho, se o subsistema do disco estiver operando acima ou próximo do limite de E/S.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para alterar o tempo de recuperação de destino**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Expanda o contêiner **Bancos de dados**. Em seguida, clique com o botão direito do mouse no banco de dados a ser alterado e clique no comando **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Banco de Dados** , clique na página **Opções** .  
  
4.  No painel **Recuperação**, no campo **Tempo de Recuperação de Destino (Segundos)** , especifique o número de segundos desejado como o limite superior do tempo de recuperação deste banco de dados.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para alterar o tempo de recuperação de destino**  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o banco de dados reside.  
  
2.  Use a instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) da seguinte maneira:  
  
     TARGET_RECOVERY_TIME **=** _target_recovery_time_ { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     A partir do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)], o valor padrão é de 1 minuto. Quando maior que 0 (o padrão para versões mais antigas) especifica o limite superior do tempo de recuperação para o banco de dados especificado no caso de uma falha.  
  
     SECONDS  
     Indica que *target_recovery_time* é expresso como o número de segundos.  
  
     MINUTES  
     Indica que *target_recovery_time* é expresso como o número de minutos.  
  
     O exemplo a seguir define o tempo de recuperação de destino do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como `60` segundos.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
