## <a name="pacemakerNotify"></a>Entender o agente de recursos do SQL Server para pacemaker

Antes da versão do CTP 1.4, o agente de recursos Pacemaker para grupos de disponibilidade não conseguia saber se uma réplica marcada como `SYNCHRONOUS_COMMIT` realmente estava atualizada ou não. É possível que a sincronização da réplica com a primária tivesse sido interrompida sem que a réplica estivesse ciente disso. Dessa forma, o agente podia promover uma réplica desatualizada para primária, o que, se bem-sucedido, causaria perda de dados. 

O SQL Server 2017 CTP 1.4 adicionou `sequence_number` ao `sys.availability_groups` para resolver esse problema. `sequence_number` é um BIGINT de crescimento monotônico que representa o quanto a réplica do grupo de disponibilidade local está atualizada em relação ao restante das réplicas do grupo de disponibilidade. A execução de failovers, a adição ou a remoção de réplicas e outras operações do grupo de disponibilidade atualizam esse número. O número é atualizado na réplica primária e então enviado por push para réplicas secundárias. Portanto, uma réplica secundária que está atualizada terá o mesmo sequence_number que a primária. 

Quando o Pacemaker decide promover uma réplica para primária, ele primeiro envia uma notificação para todas as réplicas para extrair o número de sequência e armazená-lo (chamamos isso de notificação pré-promoção). Em seguida, quando o Pacemaker realmente tentar promover uma réplica para primária, a réplica apenas promoverá a própria se o seu número de sequência for o mais alto de todos os números de sequência dentre todas as réplicas, caso contrário ela rejeitará a operação. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados. 

Observe só há garantia de que isso funcione se pelo menos uma réplica disponível para promoção tiver o mesmo número de sequência que a primária anterior. Para garantir isso, o comportamento padrão do agente de recursos do Pacemaker é definir automaticamente `REQUIRED_COPIES_TO_COMMIT`, de forma que pelo menos uma réplica secundária de confirmação síncrona seja atualizada e esteja disponível como o destino de um failover automático. Com cada ação de monitoramento, o valor de `REQUIRED_COPIES_TO_COMMIT` é calculado (e atualizado, se necessário) como (“número de réplicas de confirmação síncronas” / 2). Depois, no momento do failover, o agente de recurso exigirá (`total number of replicas` - `required_copies_to_commit` réplicas) para responder à notificação de pré-promoção para promover uma delas como primária. A réplica com o `sequence_number` mais alto será promovida a primária. 

Por exemplo, consideraremos o caso de um grupo de disponibilidade com três réplicas síncronas – uma réplica primária e duas réplicas secundárias de confirmação síncrona.

- `REQUIRED_COPIES_TO_COMMIT` é 3 / 2 = 1

- O número necessário de réplicas para responder à ação de pré-promoção é 3 - 1 = 2. Assim, 2 réplicas precisam estar ativas para o failover ser disparado. Isso significa que, em caso de interrupção primária, se uma das réplicas secundárias não estiver respondendo e somente uma das réplicas secundárias responder à ação de pré-promoção, o agente de recursos não poderá garantir que a secundária que respondeu tem o sequence_number mais alto e um failover não será disparado.

Um usuário pode optar por substituir o comportamento padrão e configurar o recurso de grupo de disponibilidade para não definir `REQUIRED_COPIES_TO_COMMIT` automaticamente como acima.

>[!IMPORTANT]
>Quando `REQUIRED_COPIES_TO_COMMIT` é 0, há risco de perda de dados. Em caso de uma interrupção da primária, o agente de recursos não disparará um failover automaticamente. O usuário precisa decidir se deseja aguardar que a primária se recupere ou fazer failover manualmente.

Para definir `REQUIRED_COPIES_TO_COMMIT` como 0, execute:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

O comando equivalente, usando crm (no SLES), é:

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

Para reverter para o valor padrão calculado, execute:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>Atualizar as propriedades do recurso faz com que todas as réplicas parem e reiniciem. Isso significa que a primária será temporariamente rebaixada para secundária e promovida novamente, o que causará indisponibilidade temporária de gravação. O novo valor para REQUIRED_COPIES_TO_COMMIT será definido apenas depois que as réplicas forem reiniciadas, portanto, não será instantâneo com a execução do comando pcs.

## <a name="balancing-high-availability-and-data-protection"></a>Balancear alta disponibilidade e proteção de dados 

O comportamento padrão acima também se aplica em caso de 2 réplicas síncronas (primária + secundária). O padrão do Pacemaker será `REQUIRED_COPIES_TO_COMMIT = 1` para garantir que a réplica secundária esteja atualizada para máxima proteção de dados.  

>[!WARNING]
>Isso oferece um risco maior de indisponibilidade da réplica primária devido a interrupções planejadas ou não na secundária. O usuário pode optar por alterar o comportamento padrão do agente de recursos e substituir o `REQUIRED_COPIES_TO_COMMIT` para 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Quando substituído, o agente de recursos vai usar a nova configuração para `REQUIRED_COPIES_TO_COMMIT` e parar de computá-la. Isso significa que os usuários terão de atualizá-la manualmente de acordo com a demanda (por exemplo, se o número de réplicas aumentar).

As tabelas abaixo descrevem o resultado de uma interrupção para réplicas primárias ou secundárias em diferentes configurações de recursos do grupo de disponibilidade:

### <a name="availability-group---2-sync-replicas"></a>Grupo de disponibilidade – 2 réplicas de sincronização

| |Interrupção principal |Interrupção de uma réplica secundária
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|O usuário deve emitir um FAILOVER manual. <br>Pode ocorrer perda de dados.<br> A nova primária é R/W |A primária é R/W, a execução está exposta a perda de dados
|`REQUIRED_COPIES_TO_COMMIT=1` * |O cluster emitirá FAILOVER automaticamente <br>Sem perda de dados. <br> A nova primária rejeitará todas as conexões até que a antiga primária se recupere e ingresse no grupo de disponibilidade como secundária. |A primária rejeitará todas as conexões até a secundária se recuperar.

\* Comportamento padrão do agente de recursos do SQL Server para Pacemaker.

### <a name="availability-group---3-sync-replicas"></a>Grupo de disponibilidade – 3 réplicas de sincronização

| |Interrupção principal |Interrupção de uma réplica secundária
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|O usuário deve emitir um FAILOVER manual. <br>Pode ocorrer perda de dados. <br>A nova primária é R/W |A primária é R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |O cluster emitirá FAILOVER automaticamente. <br>Sem perda de dados. <br>A nova primária é RW |A primária é R/W 

\* Comportamento padrão do agente de recursos do SQL Server para Pacemaker.