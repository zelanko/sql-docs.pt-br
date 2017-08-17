---
title: "Opção de failover de detecção de integridade do banco de dados | Microsoft Docs"
ms.custom: 
ms.date: 04/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- AlwaysOn
- DB_FAILOVER
- Always On
- High Availability
- SQL Server
ms.assetid: d74afd28-25c3-48a1-bc3f-e353bee615c2
caps.latest.revision: 4
author: JasonWHowell
ms.author: jasonh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 795c6bfbf7052d5747c6924b706907406c099ac0
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="availability-group-database-level-health-detection-failover-option"></a>Opção de failover de detecção de integridade no nível do banco de dados do grupo de disponibilidade

A partir do SQL Server 2016, a opção (DB_FAILOVER) de detecção de integridade no nível do banco de dados está disponível ao configurar um grupo de disponibilidade AlwaysOn. A detecção de integridade no nível do banco de dados informa quando um banco de dados não está mais no status online e quando algo deu errado e disparará o failover automático do grupo de disponibilidade. 

A detecção de integridade no nível do banco de dados está habilitada no grupo de disponibilidade como um todo e, portanto, a detecção de integridade no nível do banco de dados monitora cada banco de dados no grupo de disponibilidade. Ela não pode ser habilitada seletivamente em bancos de dados específicos no grupo de disponibilidade. 

## <a name="benefits-of-database-level-health-detection-option"></a>Benefícios da opção de detecção de integridade no nível do banco de dados
---
A opção de detecção de integridade no nível do banco de dados do grupo de disponibilidade é amplamente recomendada como uma boa opção para ajudar a garantir a alta disponibilidade dos bancos de dados. Considere a possibilidade de ativá-la em todos os grupos de disponibilidade. Se o aplicativo depender de vários bancos de dados para estar altamente disponível, agrupe-os em um grupo de disponibilidade com a opção de integridade do banco de dados ativada.

Por exemplo, com a opção de detecção de integridade no nível do banco de dados ativada, se o SQL Server não conseguir gravar no arquivo de log de transações de um dos bancos de dados, o status desse banco de dados será alterado para indicar uma falha e o grupo de disponibilidade fará failover em breve. Além disso, o aplicativo poderá se reconectar e continuar trabalhando com interrupção mínima quando os bancos de dados estiverem online novamente.

<a name="enabling-database-level-health-detection"></a>Habilitando a detecção de integridade no nível do banco de dados
----
Embora geralmente seja recomendada, a opção Integridade do Banco de Dados está **desativada por padrão**, em um esforço para manter a compatibilidade das configurações padrão em versões anteriores. 

Há várias maneiras fáceis de habilitar a configuração de detecção de integridade no nível do banco de dados:

1. No SQL Server Management Studio, conecte-se ao mecanismo de banco de dados do SQL Server. Usando a janela Pesquisador de Objetos, clique com o botão direito do mouse no nó Alta Disponibilidade AlwaysOn e execute o **Assistente de Novo Grupo de Disponibilidade**. Marque a caixa de seleção **Detecção de Integridade no Nível do Banco de Dados** na página Especificar Nome. Em seguida, conclua o restante das páginas do assistente. 

   ![Caixa de seleção Habilitar Integridade do Banco de Dados do AlwaysOn](../../../database-engine/availability-groups/windows/media/always-on-enable-database-health-checkbox.png)

2. Exiba as **Propriedades** de um Grupo de Disponibilidade existente no SQL Server Management Studio. Conecte-se ao SQL Server. Usando a janela Pesquisador de Objetos, expanda o nó Alta Disponibilidade AlwaysOn. Expanda Grupos de Disponibilidade. Clique com o botão direito do mouse no grupo de disponibilidade e escolha Propriedades. Marque a opção **Detecção de Integridade no Nível do Banco de Dados** e, em seguida, clique em OK ou em Criar script da alteração. 

   ![Detecção de Integridade no Nível do Banco de Dados nas propriedades do AG AlwaysOn](../../../database-engine/availability-groups/windows/media/always-on-ag-properties-database-level-health-detection.png)


3. Sintaxe do Transact-SQL de **CREATE AVAILABILITY GROUP**. O parâmetro DB_FAILOVER aceita valores ON ou OFF.

   ```Transact-SQL
   CREATE AVAILABILITY GROUP [Contoso-ag] 
   WITH (DB_FAILOVER=ON)
   FOR DATABASE [AutoHa-Sample] 
   REPLICA ON 
       N'SQLSERVER-0' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-0.DOMAIN.COM:5022', 
         FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT), 
       N'SQLSERVER-1' WITH (ENDPOINT_URL = N'TCP://SQLSERVER-1.DOMAIN.COM:5022',  
        FAILOVER_MODE = AUTOMATIC, AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
    ```

4. Sintaxe do Transact-SQL de **ALTER AVAILABILITY GROUP**. O parâmetro DB_FAILOVER aceita valores ON ou OFF.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = ON);
   
   ALTER AVAILABILITY GROUP [Contoso-ag] SET (DB_FAILOVER = OFF);
   ```

### <a name="caveats"></a>Advertências

É importante observar que, atualmente, a opção Detecção de Integridade no Nível do Banco de Dados não faz com que o SQL Server monitore o tempo de atividade de disco e o SQL Server não monitora diretamente a disponibilidade do arquivo de banco de dados. Caso uma unidade de disco falhe ou não esteja disponível, isso por si só não necessariamente disparará o grupo de disponibilidade para fazer failover de modo automático. 

Por exemplo, quando um banco de dados está ocioso sem nenhuma transação ativa e não está ocorrendo nenhuma gravação física, caso alguns dos arquivos do banco de dados fiquem inacessíveis, o SQL Server poderá não executar a E/S de leitura ou gravação para os arquivos nem alterar o status desse banco de dados imediatamente e, portanto, nenhum failover será disparado. Posteriormente, quando ocorrer um ponto de verificação do banco de dados ou ocorrer uma leitura ou gravação física para atender a uma consulta, o SQL Server poderá perceber o problema de arquivo e responder alterando o status do banco de dados e, mais tarde, o grupo de disponibilidade com a detecção de integridade no nível do banco de dados definida como ativada fará failover devido à alteração da integridade do banco de dados.

Como outro exemplo, quando o mecanismo de banco de dados do SQL Server precisar ler uma página de dados para atender a uma consulta, se a página de dados estiver armazenada em cache na memória do pool de buffers, nenhuma leitura de disco com acesso físico poderá ser necessária para atender à solicitação de consulta. Portanto, um arquivo de dados ausente ou não disponível poderá não disparar um failover automático imediatamente, mesmo quando a opção de integridade do banco de dados estiver habilitada, já que o status do banco de dados não está imediatamente.  


## <a name="database-failover-is-separate-from-flexible-failover-policy"></a>O failover de banco de dados é separado da política de failover flexível 
A detecção de integridade no nível do banco de dados implementa uma política de failover flexível que configura os limites da integridade do processo do SQL Server para a política de failover. A detecção de integridade no nível do banco de dados é configurada com o parâmetro DB_FAILOVER, enquanto a opção de grupo de disponibilidade FAILURE_CONDITION_LEVEL é separada para configurar a detecção de integridade do processo do SQL Server. As duas opções são independentes.

## <a name="managing-and-monitoring-database-level-health-detection"></a>Gerenciando e monitorando a detecção de integridade no nível do banco de dados

### <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico

A DMV do sistema sys.availability_groups mostra uma coluna db_failover que indica se a opção de detecção de integridade no nível do banco de dados está desativada (0) ou ativada (1).

```Transact-SQL
select name, db_failover from sys.availability_groups
```


Saída de DMV de exemplo:

name  |  db_failover  
---------|---------
| Contoso-ag |  1  |

### <a name="errorlog"></a>ErrorLog 
O Log de erros do SQL Server (ou o texto de sp_readerrorlog) mostrará a mensagem de erro 41653 quando um grupo de disponibilidade tiver feito failover, devido às verificações de detecção de integridade no nível do banco de dados. 

Por exemplo, esse trecho do log de erros mostra que uma gravação do log de transações falhou devido a um problema de disco e, posteriormente, o banco de dados chamado AutoHa-Sample foi desligado, o que disparou a detecção de integridade no nível do banco de dados para fazer failover do grupo de disponibilidade.  

>2016-04-25 12:20:21.08 spid1s      Erro: 17053, Severidade: 16, Estado: 1.
>
>2016-04-25 12:20:21.08 spid1s      SQLServerLogMgr::LogWriter: encontrado erro do sistema operacional 21 (o dispositivo não está pronto).
>2016-04-25 12:20:21.08 spid1s      Erro de gravação durante a liberação de log.
>
>2016-04-25 12:20:21.08 spid79      Erro: 9001, Severidade: 21, Estado: 4.
>
>2016-04-25 12:20:21.08 spid79      O log do banco de dados “AutoHa-Sample” não está disponível. Verifique o log de eventos para obter as mensagens de erro relacionadas. Resolva todos os erros e reinicie o banco de dados.
>
>**2016-04-25 12:20:21.15 spid79      Erro: 41653, Severidade: 21, Estado: 1.**
>
>**2016-04-25 12:20:21.15 spid79      O banco de dados “AutoHa-Sample” encontrou um erro (tipo de erro: 2 “DB_SHUTDOWN”), causando uma falha do grupo de disponibilidade “Contoso-ag”.  Consulte o log de erros do SQL Server para obter informações sobre os erros encontrados.  Se essa condição persistir, contate o administrador do sistema.**
>
>2016-04-25 12:20:21.17 spid79      Informações de estado do banco de dados “AutoHa-Sample” – LSN protegido: “(34:664:1)”    LSN de confirmação: “(34:656:1)”    Tempo de confirmação: “Apr 25 2016 12:19PM”
>
>2016-04-25 12:20:21.19 spid15s     Conexão dos Grupos de Disponibilidade AlwaysOn com o banco de dados secundário encerrada para o banco de dados primário “AutoHa-Sample” na réplica de disponibilidade “SQLServer-0” com a ID da Réplica: {c4ad5ea4-8a99-41fa-893e-189154c24b49}. Essa mensagem é apenas informativa. Não é necessária nenhuma ação do usuário.
>
>2016-04-25 12:20:21.21 spid75      AlwaysOn: a réplica local do grupo de disponibilidade “Contoso-ag” está se preparando para fazer a transição para a função de resolução, em resposta a uma solicitação do cluster WSFC (Clustering de Failover do Windows Server). Essa mensagem é apenas informativa. Não é necessária nenhuma ação do usuário.
>
>2016-04-25 12:20:21.21 spid75      O estado da réplica de disponibilidade local no grupo de disponibilidade “ag” foi alterado de “PRIMARY_NORMAL” para “RESOLVING_NORMAL”.  O estado foi alterado porque o grupo de disponibilidade sendo colocado offline.  A réplica está sendo colocada offline porque o grupo de disponibilidade associado foi excluído, porque o usuário colocou o grupo de disponibilidade associado offline no console de gerenciamento do WSFC (Clustering de Failover do Windows Server) ou porque o grupo de disponibilidade está fazendo failover para outra instância do SQL Server.  Para obter mais informações, consulte o log de erros do SQL Server, o console de gerenciamento do WSFC (Clustering de Failover do Windows Server) ou o log do WSFC.

### <a name="extended-event-sqlserveravailabilityreplicadatabasefaultreporting"></a>Evento Estendido sqlserver.availability_replica_database_fault_reporting

Há um novo Evento Estendido definido a partir do SQL Server 2016, que é disparado pela detecção de integridade no nível do banco de dados.  O nome do evento é **sqlserver.availability_replica_database_fault_reporting** 

Esse XEvent é disparado somente na réplica primária. Esse XEvent é disparado quando um problema de integridade no nível do banco de dados é detectado em um banco de dados hospedado em um grupo de disponibilidade. 

Este é um exemplo para criar uma sessão de XEvent que captura esse evento. Como nenhum caminho é especificado, o arquivo de saída de XEvent deve estar localizado no caminho do log de erros padrão do SQL Server. Execute isto na réplica primária do grupo de disponibilidade:

Script de exemplo da sessão de evento estendido
```
CREATE EVENT SESSION [AlwaysOn_dbfault] ON SERVER 
ADD EVENT sqlserver.availability_replica_database_fault_reporting
ADD TARGET package0.event_file(SET filename=N'dbfault.xel',max_file_size=(5),max_rollover_files=(4))
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,
    MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO 
ALTER EVENT SESSION AlwaysOn_dbfault ON SERVER STATE=START
GO 
```

#### <a name="extended-event-output"></a>Saída de evento estendido
Usando o SQL Server Management Studio, conecte-se ao SQL Server primário, expanda o nó Gerenciamento e, depois, expanda Eventos Estendidos. Localize a sessão (AlwaysOn_dbfault era o nome na amostra acima) e expanda-a para ver os arquivos de saída. Clique no arquivo de saída e o arquivo de evento será aberto em uma nova guia.

Explicação sobre os campos:

|Dados de coluna    | Description
|---------|---------
|availability_group_id  |A ID do grupo de disponibilidade.
|availability_group_name    |O nome do grupo de disponibilidade.
|availability_replica_id    |A ID da réplica de disponibilidade.
|availability_replica_name  |O nome da réplica de disponibilidade.
|database_name  |O nome do banco de dados que relata a falha.
|database_replica_id    |A ID do banco de dados de réplica de disponibilidade.
|failover_ready_replicas    |O número de réplicas secundárias de failover automático que são sincronizadas. 
|fault_type     | A ID de falha relatada. Valores possíveis:  <br/> 0 – NONE <br/>1 – Desconhecido<br/>2 – Desligamento
|is_critical    | Esse valor deve sempre retornar verdadeiro para o XEvent, a partir do SQL Server 2016.


Nesta saída de exemplo, o fault_type mostra que ocorreu um evento crítico no grupo de disponibilidade Contoso-ag, na réplica chamada SQLSERVER-1, devido ao banco de dados chamado AutoHa-Sample2, com o tipo de falha 2 – Desligamento.

|Campo  | Valor
|---------|---------
|availability_group_id |    24E6FE58-5EE8-4C4E-9746-491CFBB208C1
|availability_group_name |  Contoso-ag
|availability_replica_id    | 3EAE74D1-A22F-4D9F-8E9A-DEFF99B1F4D1
|availability_replica_name |    SQLSERVER-1
|database_name |    AutoHa-Sample2
|database_replica_id | 39971379-8161-4607-82E7-098590E5AE00
|failover_ready_replicas |  1
|fault_type |   2
|is_critical    | Verdadeiro


### <a name="related-references"></a>Referências relacionadas

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)

* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)

* [Política de failover flexível para failover automático de um grupo de disponibilidade (SQL Server)](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)

* [Melhorar a política de failover do AlwaysOn para testar unidades de dados e de log do Banco de Dados do SQL Server](https://blogs.msdn.microsoft.com/alwaysonpro/2016/01/14/enhance-alwayson-failover-policy-to-test-sql-server-database-data-and-log-drives/)

* [Eventos estendidos](../../../relational-databases/extended-events/extended-events.md)




