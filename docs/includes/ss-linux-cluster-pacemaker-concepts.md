## <a name="pacemakerNotify"></a>Entender o agente de recursos do SQL Server para pacemaker

Antes da versão CTP 1.4, o agente de recursos Pacemaker para grupos de disponibilidade não foi possível saber se uma réplica é marcada como `SYNCHRONOUS_COMMIT` foi realmente atualizado ou não. É possível que a sincronização da réplica com a primária tivesse sido interrompida sem que a réplica estivesse ciente disso. Assim, o agente pode promover uma réplica desatualizada para o primário - que, se for bem-sucedido, causa perda de dados. 

SQL Server 2017 CTP 1.4 adicionado `sequence_number` para `sys.availability_groups` para resolver esse problema. `sequence_number`é um BIGINT aumentando de forma monotônica que representa atualizado como a réplica do grupo de disponibilidade local é em relação ao restante das réplicas de grupo de disponibilidade. Executar failovers, adicionando ou removendo réplicas e outras operações do grupo de disponibilidade atualizar esse número. O número é atualizado na réplica primária e enviados por push para réplicas secundárias. Portanto, uma réplica secundária que está atualizada terá o mesmo sequence_number do primário. 

Quando decide Pacemaker promover uma réplica primária, ele primeiro envia uma notificação para todas as réplicas para extrair o número de sequência e armazená-lo (chamamos isso de promover previamente notificação). Em seguida, quando na verdade tenta Pacemaker promover uma réplica primária, a réplica apenas promove próprio se seu número de sequência é o mais alto de todos os números de sequência de todas as réplicas e rejeita a operação de promoção caso contrário. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados. 

Observe só há garantia de que isso funcione se pelo menos uma réplica disponível para promoção tiver o mesmo número de sequência que a primária anterior. Para garantir isso, o comportamento padrão é o agente de recurso Pacemaker definir automaticamente `REQUIRED_COPIES_TO_COMMIT` , de forma que pelo menos um síncrono confirmar secundário réplica é atualizado e disponível para ser o destino de um failover automático. Com cada ação de monitoramento, o valor de `REQUIRED_COPIES_TO_COMMIT` calculada (e atualizados, se necessário) como ('número de réplicas de confirmação síncrona' / 2). Em seguida, no momento do failover, o agente de recurso exigirá (`total number of replicas`  -  `required_copies_to_commit` réplicas) para responder à promover previamente notificação para ser capaz de promover um para primário. A réplica com o mais alto `sequence_number` será promovido a primário. 

Por exemplo, vamos considerar o caso de um grupo de disponibilidade com três réplicas síncronas - uma réplica primária e duas réplicas secundárias de confirmação síncrona.

- `REQUIRED_COPIES_TO_COMMIT`é 3 / 2 = 1

- O número necessário de réplicas para responder para promover previamente a ação é 3-1 = 2. Até 2 réplicas precisam ser para o failover deve ser disparada. Isso significa que, no caso de interrupção primária, se uma das réplicas de secundário não está respondendo e somente um dos secundários responde a promover previamente ação, o agente de recursos não pode garantir que o secundário que respondeu tem o sequence_number mais alto e um failover não será disparado.

Um usuário pode optar por substituir o comportamento padrão e configurar o recurso de grupo de disponibilidade não definir `REQUIRED_COPIES_TO_COMMIT` automaticamente como acima.

>[!IMPORTANT]
>Quando `REQUIRED_COPIES_TO_COMMIT` é lá 0 é o risco de perda de dados. No caso de uma interrupção do primário, o agente de recursos não disparará automaticamente um failover. O usuário tem que decidir se deseja aguardar principal para recuperar ou failover manual.

Para definir `REQUIRED_COPIES_TO_COMMIT` como 0, execute:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Para reverter para padrão valor calculado, execute:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=
```

>[!NOTE]
>Propriedades do recurso de atualização faz com que todas as réplicas parar e reiniciar. Isso significa primária será temporariamente rebaixada secundário, e promovida novamente que irá causar temporário escrever indisponibilidade. O novo valor para REQUIRED_COPIES_TO_COMMIT será ser definido apenas uma vez réplicas forem reiniciadas, portanto, não será instantânea com a execução do comando de pcs.

## <a name="balancing-high-availability-and-data-protection"></a>Balanceamento de alta disponibilidade e proteção de dados 

O comportamento padrão acima também se aplica ao caso de 2 réplicas síncronas (primários + secundários). O padrão será pacemaker `REQUIRED_COPIES_TO_COMMIT = 1` para garantir que o secundário réplica sempre é atualizada para proteção de dados máximo.  

>[!WARNING]
>Isso é fornecido com um risco maior de indisponibilidade da réplica primária devido a interrupções planejadas ou no secundário. O usuário pode optar por alterar o comportamento padrão do agente de recurso e substituir o `REQUIRED_COPIES_TO_COMMIT` como 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Quando substituído, o agente de recursos usará a nova configuração para `REQUIRED_COPIES_TO_COMMIT` e parar a computação-lo. Isso significa que os usuários tenham atualizá-lo manualmente adequadamente (por exemplo, se elas aumentam o número de réplicas).

As tabelas a seguir descreve o resultado de uma interrupção para réplicas primárias ou secundárias em configurações de recurso de grupo de disponibilidade diferente:

### <a name="availability-group---2-sync-replicas"></a>Grupo de disponibilidade - 2 réplicas de sincronização

| |Interrupção principal |Interrupção de uma réplica secundária
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Usuário deve emitir um FAILOVER manual. <br>Pode ter a perda de dados.<br> Novo primário é R/W |É primário R/W, em execução exposto a perda de dados
|`REQUIRED_COPIES_TO_COMMIT=1` * |Cluster emitirão automaticamente o FAILOVER <br>Sem perda de dados. <br> Novo primário irá rejeitar todas as conexões até que o antigo primário recupera e associa o grupo de disponibilidade secundário. |Primária irá rejeitar todas as conexões até recupera secundária.

\*Agente de recursos do SQL Server para o comportamento padrão de Pacemaker.

### <a name="availability-group---3-sync-replicas"></a>Grupo de disponibilidade - 3 réplicas de sincronização

| |Interrupção principal |Interrupção de uma réplica secundária
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Usuário deve emitir um FAILOVER manual. <br>Pode ter a perda de dados. <br>Novo primário é R/W |Primário é R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |Cluster emitirão automaticamente o FAILOVER. <br>Sem perda de dados. <br>Novo primário é RW |Primário é R/W 

\*Agente de recursos do SQL Server para o comportamento padrão de Pacemaker.