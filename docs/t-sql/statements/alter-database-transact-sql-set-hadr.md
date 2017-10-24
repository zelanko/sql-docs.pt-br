---
title: ALTER DATABASE SET HADR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET HADR
- SET_HADR_TSQL
- HADR_TSQL
- HADR
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE statement, AlwaysOn Availability Group
- ALTER DATABASE statement, SET HADR options
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
- Availability Groups [SQL Server], databases
ms.assetid: 20e6e803-d6d5-48d5-b626-d1e0a73d174c
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3799bc24ab3cfa9f0d65c961f69b72210c6cccef
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-transact-sql-set-hadr"></a>Alterar HADR de conjunto de banco de dados (Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico contém a sintaxe ALTER DATABASE para configuração [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] opções em um banco de dados secundário. Somente uma opção SET HADR é permitida por instrução ALTER DATABASE. Há suporte para essas opções somente em réplicas secundárias.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER DATABASE database_name  
   SET HADR   
   {  
        { AVAILABILITY GROUP = group_name | OFF }  
   | { SUSPEND | RESUME }  
   }  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados secundário a ser modificado.  
  
 SET HADR  
 Executa o comando [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] especificado no banco de dados especificado.  
  
 {O grupo de disponibilidade  **=**  *group_name* | OFF}  
 Une ou remove o banco de dados de disponibilidade no grupo de disponibilidade especificado, da seguinte forma:  
  
 *nome_do_grupo*  
 Une o banco de dados especificado na réplica secundária que é hospedada pela instância de servidor na qual você executa o comando para o grupo de disponibilidade especificado por group_name.  
  
 Os pré-requisitos para essa operação são:  
  
-   O banco de dados já deve ter sido adicionado ao grupo de disponibilidade na réplica primária.  
  
-   A réplica primária deve estar ativa. Para obter informações sobre como solucionar problemas de uma réplica primária inativa, consulte [de solução de problemas sempre em grupos de configuração de disponibilidade (SQL Server)](http://go.microsoft.com/fwlink/?LinkId=225834).  
  
-   A réplica primária deve estar online, e a réplica secundária deve estar conectada à réplica primária.  
  
-   O banco de dados secundário deve ter sido restaurado usando WITH NORECOVERY de backups de banco de dados e de log recentes do banco de dados primário, terminando com um backup de log recente o suficiente para permitir que o banco de dados secundário fique equiparado ao banco de dados primário.  
  
    > [!NOTE]  
    >  Para adicionar um banco de dados para o grupo de disponibilidade, conecte-se à instância do servidor que hospeda a réplica primária e use o [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* Adicionar banco de dados *database_name*  instrução.  
  
 Para obter mais informações, veja [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
 OFF  
 Remove o banco de dados secundário especificado do grupo de disponibilidade.  
  
 Remover um banco de dados secundário pode ser útil caso ele fique muito atrás do banco de dados primário e você não deseje esperar pelo banco de dados secundário ficar em dia. Depois de remover o banco de dados secundário, você pode atualizá-lo restaurando uma sequência de backups que terminem com um backup de log recente (usando RESTORE... WITH NORECOVERY).  
  
> [!IMPORTANT]  
>  Para remover completamente um banco de dados de disponibilidade de um grupo de disponibilidade, conecte-se à instância do servidor que hospeda a réplica primária e use o [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)*group_name* remover Banco de dados *availability_database_name* instrução. Para obter mais informações, consulte [remover um banco de dados primário de um grupo de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 SUSPEND  
 Suspende a movimentação de dados em um banco de dados secundário. O comando SUSPEND retorna assim que é aceito pela réplica que hospeda o banco de dados de destino, mas, na verdade, a suspensão do banco de dados ocorre de forma assíncrona.  
  
 O escopo do impacto depende de onde você executa a instrução ALTER DATABASE:  
  
-   Se você suspender um banco de dados secundário em uma réplica secundária, somente o banco de dados secundário local será suspenso. Conexões existentes nas secundários legíveis permanecem utilizáveis. Novas conexões para o banco de dados suspenso na secundário legível não serão permitidas até que o movimento de dados seja continuado.  
  
-   Se você suspender um banco de dados na réplica primária, a movimentação de dados será suspenso para os bancos de dados secundários correspondentes em cada réplica secundária. As conexões existentes em um secundário legível permanecem utilizáveis e novas conexões de intenção de leitura não se conectará a réplicas secundárias legíveis.  
  
-   Quando o movimento de dados é suspenso devido a um failover manual forçado, as conexões com a nova réplica secundária não são permitidas enquanto o movimento de dados estiver suspenso.  
  
 Quando um banco de dados em uma réplica secundária é suspenso, o banco de dados e a réplica se tornam não sincronizado e são marcados como NOT SYNCHRONIZED.  
  
> [!IMPORTANT]  
>  Enquanto um banco de dados secundário permanece suspenso, a fila de envio do banco de dados primário correspondente acumula registros de log de transação não enviados. As conexões para a réplica secundária retornam dados que estavam disponíveis no momento em que o movimento de dados foi suspenso.  
  
> [!NOTE]  
>  Suspender e retomar um sempre no banco de dados secundário não afeta diretamente a disponibilidade do banco de dados primário, embora suspender um banco de dados secundário pode afetar os recursos de redundância e failover para o banco de dados primário, até o suspenso banco de dados secundário é retomado. Isto está em contraste com o espelhamento de banco de dados, onde o estado de espelhamento é suspenso no banco de dados espelho e no banco de dados principal até que o espelhamento seja retomado. Suspender um banco de dados secundário AlwaysOn suspende o movimento de dados em todos os bancos de dados secundários correspondentes, e os recursos de failover e a redundância são eliminados para esse banco de dados até que o banco de dados primário seja retomado.  
  
 Para obter mais informações, consulte [suspender um banco de dados de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md).  
  
 RESUME  
 Retoma a movimentação de dados suspensa no banco de dados secundário especificado. O comando RESUME retorna assim que é aceito pela réplica que hospeda o banco de dados de destino, mas, na verdade, a retomada do banco de dados ocorre de forma assíncrona.  
  
 O escopo do impacto depende de onde você executa a instrução ALTER DATABASE:  
  
-   Se você retomar um banco de dados secundário em uma réplica secundária, somente o banco de dados secundário local será retomado. A movimentação de dados é retomada a menos que o banco de dados também seja suspenso na réplica primária.  
  
-   Se você retomar um banco de dados na réplica primária, a movimentação de dados será retomado para cada réplica secundária em que o banco de dados secundário correspondente não tenha sido suspenso localmente. Para retomar um banco de dados secundário que foi suspenso individualmente em uma réplica secundária, conecte à instância de servidor que hospeda réplica secundária e retome o banco de dados.  
  
     No modo da confirmação síncrona, o banco de dados muda para SYNCHRONIZING. Se nenhum outro banco de dados estiver suspenso atualmente, o estado da réplica também mudará para SYNCHRONIZING.  
  
     Para obter mais informações, consulte [Retomar um banco de dados de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md).  
  
## <a name="database-states"></a>Estados de banco de dados  
 Quando um banco de dados secundário é unido a um grupo de disponibilidade, a réplica secundária local altera o estado desse banco de dados secundário de RESTAURAR para ONLINE. Se um banco de dados secundário for removido do grupo de disponibilidade, ele retornará ao estado RESTORING pela réplica secundária local. Isso permite aplicar backups de log subsequentes do banco de dados primário a esse banco de dados secundário.  
  
## <a name="restrictions"></a>Restrições  
 Execute instruções ALTER DATABASE fora de transações e lotes.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no banco de dados. Unir um banco de dados a um grupo de disponibilidade requer associação no **db_owner** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir une o banco de dados secundário `AccountsDb1` à réplica secundária local do grupo de disponibilidade `AccountsAG`.  
  
```  
ALTER DATABASE AccountsDb1 SET HADR AVAILABILITY GROUP = AccountsAG;  
```  
  
> [!NOTE]  
>  Para ver esta instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] usada no contexto, veja [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) [Solucionar problemas de configuração de grupos de disponibilidade do AlwaysOn &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md) 
  
  

