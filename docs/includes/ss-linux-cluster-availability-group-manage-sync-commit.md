## <a name="managing-synchronous-commit-mode"></a>Gerenciar o modo de confirmação síncrona

>[!WARNING]
>Em alguns casos, um grupo de disponibilidade do SQL Server no modo de confirmação síncrona no Linux pode ser vulnerável à perda de dados. Consulte os detalhes a seguir sobre a causa e a solução alternativa para certificar-se de que a perda de dados seja evitada. Esse problema será corrigido em versões futuras.

###<a name="pacemaker-notification-for-availability-group-resource-promotion"></a>Notificação do Pacemaker para promoção de recurso do Grupo de Disponibilidade

Antes do lançamento do CTP 1.4, o agente de recursos Pacemaker para grupos de disponibilidade não tinha como saber se uma réplica marcada como `SYNCHRONOUS_COMMIT` estava realmente atualizada ou não. É possível que a sincronização da réplica com a primária tivesse sido interrompida sem que a réplica estivesse ciente disso. Assim, o agente podia promover uma réplica desatualizada para a primária – ação que, se bem-sucedida, causaria perda de dados. 

O SQL Server vNext CTP 1.4 adiciona `sequence_number` a `sys.availability_groups` para resolver esse problema. `sequence_number` é um BIGINT que aumenta de forma monotônica e que representa o grau de atualização da réplica de grupo de disponibilidade local em relação ao resto do sistema. Executar failovers, adicionar/remover réplicas e outras operações de grupo de disponibilidade atualizam esse número. O número é atualizado na primária, então é enviado por push para as secundárias. Assim, um secundário que estiver atualizado terá o mesmo número que a primária.

Quando o Pacemaker decide promover uma réplica para a primária, ele primeiro envia uma notificação para todas as réplicas para extrair o número de sequência e armazená-lo. Em seguida, quando o Pacemaker tentar efetivamente promover uma réplica para a primária, a réplica apenas se promoverá se o número de sequência dessa réplica for o mais alto de todos os números de sequência e, caso contrário, rejeitará a operação de promoção. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados.

Observe só há garantia de que isso funcione se pelo menos uma réplica disponível para promoção tiver o mesmo número de sequência que a primária anterior. Já que o agente de recursos requer que o Pacemaker envie notificações para todas as réplicas, o recurso disponibilidade precisa ser configurado com `notify=true`. Para cada recurso `ocf:mssql:ag` existente, o usuário precisará atualizar a configuração de recursos com `notify=true` antes de atualizar o pacote `mssql-server-ha` para CTP 1.4, caso contrário, o recurso entrará em estado de erro. 

### <a name="how-to-avoid-potential-for-data-loss"></a>Como evitar a possibilidade de perda de dados 

No caso a seguir, um grupo de disponibilidade ainda pode estar vulnerável a perda de dados. Em um cluster que inclui cinco nós, se há um grupo de disponibilidade com réplicas em três instâncias do SQL Server, é possível que a réplica primária e uma réplica secundária estejam à frente da outra réplica secundária. Quando elas estão à frente, o `sequence_number` em `sys.availability_groups` será maior do que nas outras réplicas. Nessa condição, se duas réplicas de perderem a conectividade com o restante do cluster, o Pacemaker poderá ver os três nós restantes como um quorum e permitir que a réplica latente se promova a primária. Nessa situação, há possibilidade de perda de dados.

O sqlVnext apresenta um novo recurso para forçar um determinado número de secundárias a estarem disponíveis antes que todas as transações possam ser confirmadas na primária. `REQUIRED_COPIES_TO_COMMIT` permite que você defina um número de réplicas que deve confirmar para logs de transação do banco de dados de réplica secundária antes que seja possível prosseguir com uma transação. Você pode usar essa opção com `CREATE AVAILABILITY GROUP` ou `ALTER AVAILABILITY GROUP`. Consulte [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx).

Para evitar a possibilidade de perda de dados descrita acima, defina `REQUIRED_COPIES_TO_COMMIT` para o número máximo de réplicas sincronizadas. Versões futuras terão lógica interna para lidar com a configuração de `REQUIRED_COPIES_TO_COMMIT` automaticamente.
Quando `REQUIRED_COPIES_TO_COMMIT` estiver definido, as transações nos bancos de dados de réplica primária aguardarão até que a transação seja confirmada no número necessário de logs de transação do banco de dados de réplica secundária síncrona. Se um número suficiente de réplicas secundárias síncronas não estiverem online, as transações serão interrompidas até que a comunicação com réplicas secundárias suficientes seja retomada.

O exemplo a seguir define um nome de grupo de disponibilidade [ag1] para `REQUIRED_COPIES_TO_COMMIT = 2`. 

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1]
SET (REQUIRED_COPIES_TO_COMMIT = 2)
```

No exemplo acima, se o grupo de disponibilidade tiver duas réplicas secundárias, ele aguardará até que ambas as réplicas secundárias reconheçam as confirmações. Se uma delas parar de responder, as transações serão bloqueadas.
