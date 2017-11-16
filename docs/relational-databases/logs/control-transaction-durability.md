---
title: "Controlar a durabilidade da transação | Microsoft Docs"
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- delayed durability
- Lazy Commit
ms.assetid: 3ac93b28-cac7-483e-a8ab-ac44e1cc1c76
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 956e9f95b95aa0ecb99477714e70ac61d29c45e0
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="control-transaction-durability"></a>Controlar a durabilidade da transação
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  As confirmações de transações do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser totalmente duráveis, o padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ou duráveis atrasadas (também conhecido como confirmação lenta).    
    
 As confirmações de transações totalmente duráveis são síncronas e relatam uma confirmação como bem-sucedida, devolvendo o controle ao cliente somente após a gravação dos registros de log da transação em disco. As confirmações de transações duráveis atrasadas são assíncronas e relatam uma confirmação como bem-sucedida antes que os registros de log da transação sejam gravados no disco. É necessário gravar as entradas de log das transações em disco para que uma transação seja durável. As transações duráveis atrasadas tornam-se duráveis quando as entradas de log de transações são liberadas para o disco.    
    
 Este tópico detalha as transações duráveis atrasadas.    
    
## <a name="full-vs-delayed-transaction-durability"></a>Durabilidade de transação completa versus Durabilidade de transação atrasada    
 A durabilidade de transações atrasadas e completas tem vantagens e desvantagens. Um aplicativo pode ter uma mistura de transações duráveis completas e atrasadas. Você deve considerar cuidadosamente as necessidades do seu negócio e como cada uma se adapta a essas necessidades.    
    
### <a name="full-transaction-durability"></a>Durabilidade de transação completa    
 As transações completamente duráveis gravam o log de transações no disco antes de devolver o controle para o cliente. Você deve usar transações completamente duráveis sempre que:    
    
-   O sistema não puder tolerar perda de dados.     
    Consulte a seção [Onde posso perder os dados?](../../relational-databases/logs/control-transaction-durability.md#bkmk_DataLoss) para obter mais informações sobre quando você pode perder alguns dos seus dados.    
    
-   O afunilamento não seja devido à latência de gravação do log de transações.    
    
 A durabilidade da transação atrasada reduz a latência devido à E/S do log mantendo os registros do log de transações na memória e gravando no log de transações em lotes, exigindo assim menos operações de E/S. A durabilidade da transação atrasada potencialmente reduz a contenção de E/S de log, reduzindo a espera no sistema.    
    
 **Garantias de durabilidade de transação completa**    
    
-   Assim que a confirmação de transação tiver êxito, as alterações feitas pela transação serão visíveis para as outras transações no sistema. Para obter mais informações sobre níveis de isolamento de transação, consulte [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) ou [Transações com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).    
    
-   A durabilidade é garantida após a confirmação. Os registros de log correspondentes são persistidos no disco antes que a confirmação de transação tenha êxito e retornam o controle para o cliente.    
    
### <a name="delayed-transaction-durability"></a>Durabilidade de transação atrasada    
 A durabilidade da transação atrasada é obtida usando gravações assíncronas de log no disco. Os registros do log de transações são mantidos em um buffer e gravados no disco quando o buffer é preenchido ou um evento liberação de buffer ocorre. A durabilidade da transação atrasada reduz a latência e a contenção dentro do sistema porque:    
    
-   O processamento da confirmação de transação não aguarda a E/S do log ser concluída e devolver o controle para o cliente.    
    
-   As transações simultâneas são menos prováveis de conter para a E/S do log; em vez disso, o buffer de log pode ser liberado para disco em partes maiores, reduzindo a contenção e aumentando a taxa de transferência.    
    
    > [!NOTE]    
    >  Você ainda poderá ter a contenção de E/S de log se houver um nível alto de simultaneidade, especialmente se você preencher o buffer do log mais rápido do que o liberar.    
    
 #### <a name="when-to-use-delayed-transaction-durability"></a>Quando usar a durabilidade de transação atrasada    
    
 Alguns dos casos em que você pode se beneficiar do uso da durabilidade de transação atrasada são:    
    
 **Você pode tolerar alguma perda de dados.**    
 Se você puder tolerar alguma perda de dados, por exemplo, nos casos em que os registros individuais não sejam críticos desde que você tenha a maioria dos dados, poderá ser válido considerar a durabilidade atrasada. Se você não puder tolerar perda de dados, não use a durabilidade de transação atrasada.    
    
 **Você está observando um afunilamento em gravações de log de transações.**    
 Se seus problemas de desempenho forem devido à latência em gravações do log de transações, seu aplicativo provavelmente se beneficiará do uso da durabilidade de transação atrasada.    
    
 **Suas cargas de trabalho têm uma taxa alta de contenção.**    
 Se o sistema tiver cargas de trabalho com um nível alto de contenção, muito tempo será perdido aguardando que os bloqueios sejam liberados. A durabilidade de transação atrasada reduz o tempo de confirmação e libera os bloqueios mais rapidamente, resultando em uma taxa de transferência mais alta.    
    
 ### <a name="delayed-transaction-durability-guarantees"></a>Garantias de durabilidade de transação atrasada   
    
-   Assim que a confirmação de transação tiver êxito, as alterações feitas pela transação serão visíveis para as outras transações no sistema.    
    
-   A durabilidade da transação é garantida apenas após uma liberação do log de transações de memória para o disco. O log de transações de memória é liberado para disco quando:    
    
    -   Uma transação completamente durável no mesmo banco de dados faz uma alteração no banco de dados e é confirmada com sucesso.   
    
    -   O usuário executa um procedimento armazenado do sistema `sp_flush_log` com sucesso.     
    
        Se uma transação completamente durável ou um sp_flush_log for confirmado com êxito, todas as transações de durabilidade atrasadas confirmadas têm a garantia de se tornarem duráveis.
        
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta liberar o log em disco com base na geração de log e no tempo, mesmo se todas as transações forem duráveis atrasadas. Em geral, isso terá êxito se o dispositivo de E/S estiver acompanhando. Contudo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornece nenhuma garantia de durabilidade rígida além das transações duráveis e sp_flush_log.      
    
  
    
## <a name="how-to-control-transaction-durability"></a>Como controlar a durabilidade da transação    
    
###  <a name="bkmk_DbControl"></a> Database level control    
 Você, o DBA, pode controlar se os usuários podem usar a durabilidade da transação atrasada em um banco de dados com a instrução a seguir. Você deve definir a configuração de durabilidade atrasada com ALTER DATABASE.    
    
```tsql    
ALTER DATABASE … SET DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }    
```    
    
 **DESABILITADO**    
 [padrão] Com essa configuração, todas as transações confirmadas no banco de dados são completamente duráveis, independentemente da configuração do nível de confirmação (DELAYED_DURABILITY=[ON | OFF]). Não há nenhuma necessidade de modificação e recompilação do procedimento armazenado. Isso permite garantir que a durabilidade atrasada nunca coloque os dados em risco.    
    
 **PERMITIDO**    
 Com essa configuração, a durabilidade de cada transação é determinada no nível da transação – DELAYED_DURABILITY = { *OFF* | ON }. Consulte [Controle no nível do bloco atômico – procedimentos armazenados e compilados nativamente](../../relational-databases/logs/control-transaction-durability.md#CompiledProcControl) e [Nível de controle COMMIT – Transact-SQL](../../relational-databases/logs/control-transaction-durability.md#bkmk_T-SQLControl) para obter mais informações.    
    
 **FORÇADO**    
 Com essa configuração, cada transação que é confirmada no banco de dados é durável atrasada. Independentemente de a transação especificar completamente durável (DELAYED_DURABILITY = OFF) ou não fizer nenhuma especificação, a transação será durável atrasada. Essa configuração é útil quando a durabilidade da transação atrasada é útil para um banco de dados e você não quer alterar o código do aplicativo.    
    
###  <a name="CompiledProcControl"></a> Atomic block level control – Natively Compiled Stored Procedures    
 O código a seguir fica dentro do bloco atômico.    
    
```tsql    
DELAYED_DURABILITY = { OFF | ON }    
```    
    
 **Desligado**    
 [padrão] A transação será completamente durável, a menos que a opção DELAYED_DURABLITY = FORCED esteja em vigor; nesse caso, a confirmação será assíncrona e, portanto, durável atrasada. Consulte [Controle de nível de banco de dados](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obter mais informações.    
    
 **Ligado**    
 A transação será durável atrasada, a menos que a opção DELAYED_DURABLITY = DISABLED esteja em vigor; nesse caso, a confirmação será síncrona e completamente durável.  Consulte [Controle de nível de banco de dados](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obter mais informações.    
    
 **Código de exemplo:**    
    
```tsql    
CREATE PROCEDURE <procedureName> …    
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER    
AS BEGIN ATOMIC WITH     
(    
    DELAYED_DURABILITY = ON,    
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,    
    LANGUAGE = N'English'    
    …    
)    
END    
```    
    
### <a name="table-1-durability-in-atomic-blocks"></a>Tabela 1: Durabilidade em blocos atômicos    
    
|Opção da durabilidade do bloco atômico|Não há transação existente|Transação em processo (completamente durável ou atrasada)|    
|------------------------------------|-----------------------------|---------------------------------------------------------|    
|**DELAYED_DURABILITY = OFF**|O bloco atômico inicia uma nova transação completamente durável.|O bloco atômico cria um ponto de salvamento na transação existente e, em seguida, inicia a nova transação.|    
|**DELAYED_DURABILITY = ON**|O bloco atômico inicia uma nova transação durável atrasada.|O bloco atômico cria um ponto de salvamento na transação existente e, em seguida, inicia a nova transação.|    
    
###  <a name="bkmk_T-SQLControl"></a> COMMIT level control –[!INCLUDE[tsql](../../includes/tsql-md.md)]    
 A sintaxe de COMMIT é estendida para que você possa forçar a durabilidade da transação atrasada. Se DELAYED_DURABILITY for DISABLED ou FORCED no nível de banco de dados (veja acima) essa opção COMMIT será ignorada.    
    
```tsql    
COMMIT [ { TRAN | TRANSACTION } ] [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]    
    
```    
    
 **Desligado**    
 [padrão] A transação COMMIT será completamente durável, a menos que a opção de banco de dados DELAYED_DURABLITY = FORCED esteja em vigor; nesse caso, a COMMIT é assíncrona e, portanto, durável atrasada. Consulte [Controle de nível de banco de dados](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obter mais informações.    
    
 **Ligado**    
 A transação COMMIT será durável atrasada, a menos que a opção de banco de dados DELAYED_DURABLITY = DISABLED esteja em vigor; nesse caso, a COMMIT é síncrona e, portanto, completamente durável. Consulte [Controle de nível de banco de dados](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obter mais informações.    
    
### <a name="summary-of-options-and-their-interactions"></a>Resumo de opções e suas interações    
 Esta tabela resume as interações entre as configurações de durabilidade atrasada de nível de banco de dados e as configurações no nível da confirmação. As configurações no nível de banco de dados sempre têm precedência sobre configurações no nível de confirmação.    
    
|Configuração de COMMIT/Configuração de banco de dados|DELAYED_DURABILITY = DISABLED|DELAYED_DURABILITY = ALLOWED|DELAYED_DURABILITY = FORCED|    
|--------------------------------------|-------------------------------------|------------------------------------|-----------------------------------|    
|**DELAYED_DURABILITY = OFF** Transações de nível de banco de dados.|A transação é completamente durável.|A transação é completamente durável.|A transação é durável atrasada.|    
|**DELAYED_DURABILITY = ON** Transações de nível de banco de dados.|A transação é completamente durável.|A transação é durável atrasada.|A transação é durável atrasada.|    
|**DELAYED_DURABILITY = OFF** Transações entre bancos de dados ou distribuídos.|A transação é completamente durável.|A transação é completamente durável.|A transação é completamente durável.|    
|**DELAYED_DURABILITY = ON** Transações entre bancos de dados ou distribuídos.|A transação é completamente durável.|A transação é completamente durável.|A transação é completamente durável.|    
    
## <a name="how-to-force-a-transaction-log-flush"></a>Como forçar uma liberação de log de transações    
 Há dois meios de forçar a liberação do log de transações para o disco.    
    
-   Executar qualquer transação completamente durável que altera o mesmo banco de dados. Isso força uma liberação para o disco dos registros de log de todas as transações de durabilidade confirmadas anteriormente.    
    
-   Executar o procedimento armazenado do sistema `sp_flush_log`. Esse procedimento força uma liberação para o disco dos registros de log de todas as transações duráveis confirmadas anteriormente. Para obter mais informações, consulte [sys.sp_flush_log &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-flush-log-transact-sql.md).    
    
##  <a name="bkmk_OtherSQLFeatures"></a> Durabilidade atrasada e outros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos    
 **Controle de alterações e alterar captura de dados**    
 Todas as transações com controle de alterações são completamente duráveis. Uma transação terá a propriedade de controle de alterações se fizer alguma operação de gravação nas tabelas que estão habilitadas para controle de alterações. Não há suporte para o uso de durabilidade atrasada para bancos de dados que usam o CDC (Change Data Capture).    
    
 **Recuperação de pane**    
 A consistência é garantida, mas algumas alterações das transações duráveis atrasadas que foram confirmadas podem ser perdidas.    
    
 **Entre bancos de dados e DTC**    
 Se uma transação for entre bancos de dados ou distribuída, ela será completamente durável, independentemente da configuração de confirmação de banco de dados ou transação.    
    
 **Grupos de Disponibilidade AlwaysOn e espelhamento**    
 As transações duráveis atrasadas não garantem nenhuma durabilidade no primário nem em nenhum dos secundários. Além disso, elas não garantem conhecimento sobre a transação no secundário. Após a confirmação, o controle é retornado para o cliente antes de qualquer reconhecimento ser recebido de algum secundário síncrono. Replicação para réplicas secundárias continua a ocorrer conforme acontece a liberação em disco no primário.   
    
 **Clustering de failover**    
 Algumas gravações de transações duráveis atrasadas podem ser perdidas.    
    
 **Replicação de transação**    
 Não há suporte para transações duráveis atrasadas com replicação transacional.    
    
 **Envio de logs**    
 Somente as transações que se tornaram duráveis são incluídas no log enviado.    
    
 **backup de log**    
 Somente as transações que se tornaram duráveis são incluídas no backup.    
    
##  <a name="bkmk_DataLoss"></a> When can I lose data?    
 Se você implementar durabilidade atrasada em qualquer de suas tabelas, você deve compreender que certas circunstâncias podem levar à perda de dados. Se você não puder tolerar perda de dados, não use a durabilidade atrasada em suas tabelas.    
    
### <a name="catastrophic-events"></a>Eventos catastróficos    
 No caso de um evento catastrófico, como uma falha do servidor, você perderá os dados de todas as transações confirmadas que não foram salvas em disco. As transações duráveis atrasadas são salvas no disco sempre que uma transação totalmente durável é executada em qualquer tabela (duráveis com otimização de memória ou baseada em disco) no banco de dados ou quando o `sp_flush_log` é chamado. Se estiver usando transações duráveis atrasadas, você pode querer criar uma pequena tabela no banco de dados que você pode atualizar periodicamente ou chamar periodicamente o `sp_flush_log` para salvar todas as transações confirmadas pendentes. O log de transações também é liberado sempre que fica cheio, mas é difícil de prever e impossível de controlar.    
    
### <a name="includessnoversionincludesssnoversion-mdmd-shutdown-and-restart"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desligamento e reinício    
 Para durabilidade atrasada, não há diferença entre um desligamento inesperado e um desligamento/reinício esperado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como os eventos catastróficos, você também deve se planejar para a perda de dados. Em um desligamento planejado/reinício, algumas transações que não foram gravadas em disco podem primeiro ser salvas em disco, mas você não deve planejar isso. Planeje mesmo se um desligamento/reinício, seja planejado ou não, perda os dados da mesma forma que um evento catastrófico.    
    
## <a name="see-also"></a>Consulte também    
 [Transações com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)    
    
  

