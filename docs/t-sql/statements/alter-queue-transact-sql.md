---
title: ALTER QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_QUEUE_TSQL
- ALTER QUEUE
dev_langs:
- TSQL
helpviewer_keywords:
- number of queue readers
- modifying queues
- ALTER QUEUE statement
- queue readers [SQL Server]
- queues [Service Broker], modifying
- unavailable queues [SQL Server]
- activation stored procedures [Service Broker]
ms.assetid: d54aa325-8761-4cd4-8da7-acf33df12296
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a336b58ed148fa135835f4d991d73644c5f1799e
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503234"
---
# <a name="alter-queue-transact-sql"></a>ALTER QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de uma fila.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER QUEUE <object>   
   queue_settings  
   | queue_action  
[ ; ]  
  
<object> : :=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
  
<queue_settings> : :=  
WITH  
   [ STATUS = { ON | OFF } [ , ] ]  
   [ RETENTION = { ON | OFF } [ , ] ]  
   [ ACTIVATION (  
       { [ STATUS = { ON | OFF } [ , ] ]   
         [ PROCEDURE_NAME = <procedure> [ , ] ]  
         [ MAX_QUEUE_READERS = max_readers [ , ] ]  
         [ EXECUTE AS { SELF | 'user_name'  | OWNER } ]  
       |  DROP }  
          ) [ , ]]  
         [ POISON_MESSAGE_HANDLING (  
          STATUS = { ON | OFF } )  
         ]   
  
<queue_action> : :=  
   REBUILD [ WITH <query_rebuild_options> ]  
   | REORGANIZE [ WITH (LOB_COMPACTION = { ON | OFF } ) ]  
   | MOVE TO { file_group | "default" }  
  
<procedure> : :=  
{ database_name.schema_name.stored_procedure_name | schema_name.stored_procedure_name | stored_procedure_name }
  
<queue_rebuild_options> : :=  
{  
   ( MAXDOP = max_degree_of_parallelism )  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* (object)  
 É o nome do banco de dados que contém a fila a ser alterada. Quando nenhum *database_name* for fornecido, o padrão será o banco de dados atual.  
  
 *schema_name* (object)  
 É o nome do esquema ao qual a nova fila pertence. Quando nenhum *schema_name* for fornecido, o padrão será o esquema padrão do usuário atual.  
  
 *queue_name*  
 É o nome da fila a ser alterada.  
  
 STATUS (Fila)  
 Especifica se a fila está disponível (ON) ou indisponível (OFF). Quando a fila estiver indisponível, nenhuma mensagem pode ser adicionada à fila ou removida dela.  
  
 RETENTION  
 Especifica a configuração de retenção para a fila. Se RETENTION = ON, todas as mensagens enviadas ou recebidas em conversas usando essa fila serão mantidas na fila até que as conversas tenham terminado. Isso permite manter as mensagens para fins de auditoria ou executar transações de compensação se ocorrer um erro.  
  
> [!NOTE]  
>  Definir RETENÇÃO = ON pode reduzir o desempenho. Essa configuração deve ser usada somente se for necessária para atender ao contrato de nível de serviço para o aplicativo.  
  
 ACTIVATION  
 Especifica as informações sobre o procedimento armazenado que é ativado ao processar as mensagens que chegam nessa fila.  
  
 STATUS (Ativação)  
 Especifica se a fila ativa ou não o procedimento armazenado. Quando o STATUS = ON, a fila começa o procedimento armazenado especificado com PROCEDURE_NAME quando o número de procedimentos atualmente sendo executados for menos que MAX_QUEUE_READERS e quando as mensagens chegarem à fila mais rápido do que os procedimentos armazenados recebam as mensagens. Quando o STATUS = OFF, a fila não ativa o procedimento armazenado.  
  
 REBUILD [ WITH \<queue_rebuild_options> ]  
 **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Recompila todos os índices na tabela interna da fila. Use esse recurso quando estiver com problemas de fragmentação devido à alta carga. MAXDOP é a única opção de recompilação de fila com suporte. REBUILD sempre é uma operação offline.  
  
 REORGANIZE [ WITH ( LOB_COMPACTION = { ON | OFF } ) ]  
 **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Reorganize todos os índices na tabela interna da fila.   
Ao contrário de REORGANIZE em tabelas de usuário, REORGANIZE em uma fila sempre é executada como uma operação offline porque os bloqueios no nível da página são desabilitados explicitamente nas filas.  
  
> [!TIP]  
>  Para obter as diretrizes gerais sobre a fragmentação de índice, quando a fragmentação estiver entre 5% e 30%, reorganize o índice. Quando a fragmentação estiver acima de 30%, recompile o índice. No entanto, esses números são apenas para diretrizes gerais como um ponto inicial para o seu ambiente. Para determinar a quantidade de fragmentação de índice, use [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) – confira o exemplo G neste artigo para obter exemplos.  
  
 MOVE TO { *file_group* | "default" }  
 **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Move a tabela interna da fila (com seus índices) para um grupo de arquivos especificado pelo usuário.  O novo grupo de arquivos não pode ser somente leitura.  
  
 PROCEDURE_NAME = \<procedure>  
 Especifica o nome do procedimento armazenado a ser ativado quando a fila contiver mensagens a serem processadas. Esse valor deve ser um identificador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *database_name* (procedimento)  
 É o nome do banco de dados que contém o procedimento armazenado.  
  
 *schema_name* (procedimento)  
 É o nome do esquema que é proprietário do procedimento armazenado.  
  
 *stored_procedure_name*  
 É o nome do procedimento armazenado.  
  
 MAX_QUEUE_READERS =*max_reader*  
 Especifica o número máximo de instâncias do procedimento armazenado de ativação que a fila inicia simultaneamente. O valor de *max_readers* precisa ser um número entre 0 e 32767.  
  
 EXECUTE AS  
 Especifica a conta do usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob a qual é executado o procedimento armazenado de ativação. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve poder verificar as permissões deste usuário no momento em que a fila ativa o procedimento armazenado. Para um usuário de domínio do Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar conectado ao domínio e ser capaz de validar as permissões do usuário especificado quando o procedimento for iniciado, caso contrário, a ativação falhará. Para um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o servidor sempre pode verificar as permissões.  
  
 SELF  
 Especifica que o procedimento armazenado é executado como o usuário atual. (O principal do banco de dados que executa essa instrução ALTER QUEUE.)  
  
 '*user_name*'  
 É o nome do usuário com o qual o procedimento armazenado é executado. *user_name* precisa ser um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido especificado pelo usuário como um identificador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O usuário atual precisa ter a permissão IMPERSONATE para o *user_name* especificado.  
  
 OWNER  
 Especifica que o procedimento armazenado é executado como o proprietário da fila.  
  
 DROP  
 Exclui todas as informações de ativação associadas à fila.  
  
 POISON_MESSAGE_HANDLING  
 Especifica se a manipulação de mensagens suspeitas está habilitada. O padrão é ON.  
  
 A fila que tiver a manipulação de mensagens suspeitas definida como OFF, não será desabilitada após cinco reversões consecutivas de transações. Isso permite que um sistema personalizado de manipulação de mensagens suspeitas seja definido pelo aplicativo.  
  
## <a name="remarks"></a>Remarks  
 Quando uma fila com um procedimento armazenado de ativação especificado tiver mensagens, a alteração do status de ativação de OFF para ON ativa imediatamente o procedimento armazenado de ativação. A alteração do status de ativação de ON para OFF faz o Broker parar de ativar instâncias do procedimento armazenado, mas não interrompe as instâncias do procedimento armazenado em execução atualmente.  
  
 A alteração de uma fila para adicionar um procedimento armazenado de ativação não altera o status de ativação da fila. A alteração do procedimento armazenado de ativação para a fila não afeta as instâncias do procedimento armazenado de ativação em execução atualmente.  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] verifica o número máximo de leitores de fila para uma fila como parte do processo de ativação. Portanto, alterar uma fila para aumentar o número de máximo de leitores de fila permite que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inicie imediatamente mais instâncias do procedimento armazenado de ativação. A alteração de uma fila para diminuir o número de máximo de leitores de fila não afeta as instâncias do procedimento armazenado de ativação em execução atualmente. Entretanto, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] não inicia uma nova instância do procedimento armazenado até que o número de instâncias para o procedimento armazenado de ativação seja menor que o número máximo configurado.  
  
 Quando uma fila não está disponível, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] mantém as mensagens para os serviços que usam a fila na transmissão para o banco de dados. A exibição de catálogo [sys.transmission_queue](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md) fornece uma exibição da fila de transmissão.  
  
 Se uma instrução RECEIVE ou GET CONVERSATION GROUP especificar uma fila não disponível, ela falhará com um erro [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permissões  
 A permissão para alterar uma fila assume como padrão o proprietário da fila, os membros das funções de banco de dados fixas db_ddladmin ou db_owner e os membros da função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-making-a-queue-unavailable"></a>A. Tornando uma fila não disponível  
 O exemplo a seguir torna a fila `ExpenseQueue` não disponível para receber mensagens.  
  
```  
ALTER QUEUE ExpenseQueue WITH STATUS = OFF ;  
```  
  
### <a name="b-changing-the-activation-stored-procedure"></a>B. Alterando o procedimento armazenado de ativação  
 O exemplo a seguir altera o procedimento armazenado que a fila inicia. O procedimento armazenado executa como o usuário que executou a instrução `ALTER QUEUE`.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = new_stored_proc,  
        EXECUTE AS SELF) ;  
```  
  
### <a name="c-changing-the-number-of-queue-readers"></a>C. Alterando o número de leitores da fila  
 O exemplo a seguir define como `7` o número máximo de instâncias de procedimento armazenado que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inicia para essa fila.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (MAX_QUEUE_READERS = 7) ;  
```  
  
### <a name="d-changing-the-activation-stored-procedure-and-the-execute-as-account"></a>D. Alterando o procedimento armazenado de ativação e a conta EXECUTE AS  
 O exemplo a seguir altera o procedimento armazenado que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] inicia. O procedimento armazenado executa como o usuário `SecurityAccount`.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = AdventureWorks2012.dbo.new_stored_proc ,  
        EXECUTE AS 'SecurityAccount') ;  
```  
  
### <a name="e-setting-the-queue-to-retain-messages"></a>E. Definindo a fila para reter mensagens  
 O exemplo a seguir define a fila para reter mensagens. A fila retém todas as mensagens enviadas para ou dos serviços que a utilizam, até terminar a conversa que contém a mensagem.  
  
```  
ALTER QUEUE ExpenseQueue WITH RETENTION = ON ;  
```  
  
### <a name="f-removing-activation-from-a-queue"></a>F. Removendo a ativação de uma fila  
 O exemplo a seguir remove todas as informações de ativação da fila.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (DROP) ;  
```  
  
### <a name="g-rebuilding-queue-indexes"></a>G. Recompilando índices de fila  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O exemplo a seguir recompila índices de fila  
  
```  
ALTER QUEUE ExpenseQueue REBUILD WITH (MAXDOP = 2)   
```  
  
### <a name="h-reorganizing-queue-indexes"></a>H. Reorganizando índices de fila  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O exemplo a seguir reorganiza índices de fila  
  
```  
ALTER QUEUE ExpenseQueue REORGANIZE   
```  
  
### <a name="i-moving-queue-internal-table-to-another-filegroup"></a>I: movendo a tabela interna da fila para outro grupo de arquivos  
  
**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER QUEUE ExpenseQueue MOVE TO [NewFilegroup]   
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
  
