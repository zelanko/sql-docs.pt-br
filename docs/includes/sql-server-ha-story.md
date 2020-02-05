Este artigo fornece uma visão geral das soluções de continuidade de negócios para alta disponibilidade e recuperação de desastre no SQL Server. 

Todos que implantam o SQL Server têm uma tarefa comum para levar em consideração, que é certificar-se de que todas as instâncias do SQL Server de missão crítica e os bancos de dados dentro delas estarão disponíveis quando os usuários finais e de negócios precisarem delas, independentemente de ser em horário comercial ou o tempo todo. A meta é manter os negócios em funcionamento com o mínimo ou sem qualquer interrupção. Esse conceito também é conhecido como continuidade de negócios.

O SQL Server 2017 apresenta muitos novos recursos ou aprimoramentos aos existentes, alguns dos quais são de disponibilidade. A maior adição ao 2017 do SQL Server é o suporte para SQL Server em distribuições do Linux. Para obter uma lista completa dos novos recursos no SQL Server 2017, consulte o tópico [Novidades no SQL Server](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017).

Este artigo está focado em abordar os cenários de disponibilidade no SQL Server 2017, bem como os novos e aprimorados recursos de disponibilidade no SQL Server 2017. Os cenários incluem os híbridos que serão capazes de estender as implantações do SQL Server no Windows Server e no Linux, bem como aquelas que podem aumentar o número de cópias legíveis de um banco de dados. Embora este artigo não aborde as opções de disponibilidade externas ao SQL Server, como as fornecidas pela virtualização, tudo discutido aqui se aplica às instalações do SQL Server em uma máquina virtual convidada, seja na nuvem pública ou hospedada em um servidor do hipervisor local.

## <a name="sql-server-2017-scenarios-using-the-availability-features"></a>Cenários de 2017 do SQL Server usando os recursos de disponibilidade

Os grupos de disponibilidade, FCIs e envio de logs podem ser usados de diversas formas e não necessariamente apenas para fins de disponibilidade. Os recursos de disponibilidade podem ser usados de quatro maneiras principais:

* Alta disponibilidade
* Recuperação de desastre
* Migrações e atualizações
* Expandindo cópias legíveis de um ou mais bancos de dados

Cada seção abordará os recursos relevantes que podem ser usados nesse cenário específico. O único recurso não abordado é a [replicação do SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication). Embora não seja oficialmente designado como um recurso de disponibilidade sob a cobertura do AlwaysOn, ele geralmente é usado para tornar os dados redundantes em determinados cenários. A replicação será adicionada ao SQL Server no Linux em uma versão futura.

> [!IMPORTANT] 
> Os recursos de disponibilidade do SQL Server não substituem a necessidade de ter uma estratégia de backup e restauração bem testada e robusta, o bloco de construção mais fundamental de qualquer solução de disponibilidade.

### <a name="high-availability"></a>Alta disponibilidade

É muito importante garantir que o banco de dados ou as instâncias do SQL Server estejam disponíveis caso ocorra um problema local para um data center ou uma única região na região da nuvem. Esta seção abordará como recursos de disponibilidade do SQL Server podem auxiliar nessa tarefa. Todos os recursos descritos estão disponíveis tanto no Windows Server quanto no Linux. 

#### <a name="always-on-availability-groups"></a>Grupos de disponibilidade AlwaysOn

Introduzidos no SQL Server 2012, os Grupos de Disponibilidade AlwaysOn (grupos de disponibilidade) fornecem proteção em nível de banco de dados ao enviar cada transação de um banco de dados para outra instância, conhecida como uma réplica, que contém uma cópia do banco de dados em um estado especial. Um grupo de disponibilidade pode ser implantado nas Standard ou Enterprise Editions.  As instâncias que participam de um grupo de disponibilidade podem ser autônomas ou Instâncias de Cluster de Failover AlwaysOn (FCIs, descritas na próxima seção). Como as transações são enviadas a uma réplica conforme acontecem, os grupos de disponibilidade são recomendados onde houver requisitos para o ponto de recuperação inferior e para objetivos de tempo de recuperação. A movimentação de dados entre as réplicas pode ser síncrona ou assíncrona, com a Enterprise Edition, permitindo que até três réplicas (inclusive a primária) sejam síncronas. Um grupo de disponibilidade tem uma cópia de leitura/gravação completa do banco de dados que está na réplica primária, enquanto todas as réplicas secundárias não podem receber transações diretamente de usuários finais ou de aplicativos. 

> [!NOTE] 
> AlwaysOn é um termo coletivo para os recursos de disponibilidade do SQL Server e aborda os grupos de disponibilidade e FCIs. AlwaysOn não é o nome do recurso do grupo de disponibilidade.

Como os grupos de disponibilidade fornecem apenas proteção no nível do banco de dados e não no nível de instância, nada que não seja capturado no log de transações ou configurado no banco de dados será necessário para sincronizar manualmente cada réplica secundária. Alguns exemplos de objetos que devem ser sincronizados manualmente são logons no nível de instância, servidores vinculados e trabalhos do SQL Server Agent.

Um grupo de disponibilidade também tem outro componente chamado ouvinte, que permite que aplicativos e usuários finais se conectem sem a necessidade de saber qual instância do SQL Server está hospedando a réplica primária. Cada grupo de disponibilidade deve ter seu próprio ouvinte. Enquanto as implementações do ouvinte são um pouco diferentes no Windows Server em comparação ao Linux, a funcionalidade que fornece e como é usada é a mesma. A figura abaixo mostra um grupo de disponibilidade com base no Windows Server que está usando um Cluster de Failover do Windows Server (WSFC). Um cluster subjacente na camada do sistema operacional é necessário para disponibilidade se estiver no Linux ou no Windows Server. O exemplo mostra uma configuração de dois servidores ou nós simples, na qual um WSFC é o cluster subjacente. 

![Grupo de disponibilidade simples](media/sql-server-ha-story/image1.png)
 
As Standard e Enterprise Editions têm valores máximos diferentes quando se trata de réplicas. Um grupo de disponibilidade na Standard Edition, conhecido como um Grupo de Disponibilidade Básico, dá suporte a duas réplicas (uma primária e uma secundária) com apenas um único banco de dados no grupo de disponibilidade. A Enterprise Edition não só permite que vários bancos de dados sejam configurados em um único grupo de disponibilidade, mas também pode ter até nove réplicas no total (uma primária, oito secundárias). A Enterprise Edition também fornece outros benefícios opcionais, como réplicas secundárias legíveis, a capacidade de fazer backups de uma réplica secundária e muito mais.

>[!NOTE]
> O espelhamento de banco de dados, que foi preterido no SQL Server 2012, não está disponível na versão Linux do SQL Server e também não será ser adicionado. Os clientes que ainda estão usando o espelhamento de banco de dados devem começar a planejar a migração para grupos de disponibilidade, que é a substituição de espelhamento de banco de dados.

Quando se trata de disponibilidade, os grupos de disponibilidade podem fornecer um failover automático ou manual. O failover automático poderá ocorrer se a movimentação de dados síncronos for configurada e o banco de dados na réplica primária e secundária estiverem em um estado sincronizado. Contanto que o ouvinte seja usado e o aplicativo usar uma versão posterior do .NET (3.5 com uma atualização ou 4.0 e posterior), o failover deverá ser tratado com pouco ou nenhum impacto para encerrar os usuários se um ouvinte for utilizado. O failover para tornar a nova réplica primária uma réplica secundária pode ser configurado para ser automático ou manual e geralmente é medido em segundos.

A lista a seguir destaca algumas diferenças de grupos de disponibilidade no Windows Server e no Linux:
* Devido a diferenças na maneira que o cluster subjacente funciona no Linux e no Windows Server, todos os failovers (manuais ou automáticos) de grupos de disponibilidade são feitos por meio do cluster no Linux. Em implantações do grupo de disponibilidade com base no Windows Server, os failovers manuais devem ser feitos por meio do SQL Server. Os failovers automáticos são tratados pelo cluster subjacente no Windows Server e no Linux. 
* No SQL Server 2017, a configuração recomendada para grupos de disponibilidade no Linux será um mínimo de três réplicas. Isso ocorre devido à maneira que o clustering subjacente funciona. Uma melhor solução para uma configuração de duas réplicas virá após o lançamento.
* No Linux, o nome comum usado por cada ouvinte é definido no DNS e não no cluster, como no Windows Server.

No SQL Server 2017, há alguns novos recursos e aprimoramentos para grupos de disponibilidade:

* Tipos de cluster
* REQUIRED_SECONDARIES_TO_COMMIT
* Suporte aprimorado do Coordenador de Transação do Distribuidor (DTC) da Microsoft para configurações com base no Windows Server
* Outros cenários de expansão para bancos de dados de somente leitura (descritos posteriormente neste artigo)

##### <a name="always-on-availability-group-cluster-types"></a>Tipos de cluster do grupo de disponibilidade AlwaysOn

O formulário de disponibilidade interna de clustering no Windows Server é habilitado por meio de um recurso chamado Clustering de Failover. Ele permite que você compile um WSFC para ser usado com um grupo de disponibilidade ou FCI. A integração de grupos de disponibilidade e FCIs é fornecida por DLLs de recurso com suporte a cluster entregues pelo SQL Server. 

Cada distribuição Linux com suporte entrega sua própria versão da solução de custer Pacemaker. O SQL Server 2017 no Linux dá suporte ao uso do Pacemaker. O Pacemaker é uma solução de pilha aberta. Com ele, cada distribuição pode, então, ser integrada à sua pilha. Enquanto as distribuições fornecem o Pacemaker, ele não é tão integrado quanto o recurso do Clustering de Failover no Windows Server.

Um WSFC e o Pacemaker são mais semelhantes do que diferentes. Ambos fornecem uma maneira de obter servidores individuais e combiná-los em uma configuração para fornecer disponibilidade e têm conceitos de coisas como recursos, restrições (mesmo se implementadas de maneira diferente), failover e assim por diante. A fim de dar suporte ao Pacemaker para as configurações do grupo de disponibilidade e da FCI, incluindo itens como failover automático, a Microsoft fornece o pacote mssql-server-ha, que é semelhante, mas não exatamente igual, aos DLLs de recurso em um WSFC para Pacemaker. Uma das diferenças entre um WSFC e o Pacemaker é que não há nenhum recurso de nome de rede no Pacemaker, que é o componente que ajuda a abstrair o nome do ouvinte (ou o nome da FCI) em um WSFC. O DNS fornece essa resolução de nome no Linux.

Por causa da diferença na pilha do cluster, algumas alterações precisam ser feitas para grupos de disponibilidade porque o SQL Server tem que lidar com alguns dos metadados que são nativamente tratados por um WSFC. A alteração mais [!IMPORTANT] é a introdução de um tipo de cluster para um grupo de disponibilidade. Isso é armazenado em sys. availability_groups nas colunas cluster_type e cluster_type_desc. Há três tipos de cluster:

* WSFC 
* Externo
* Nenhum

Todos os grupos de disponibilidade que exigem disponibilidade devem usar um cluster subjacente, o que no caso do SQL Server 2017 significa um WSFC ou Pacemaker. Para grupos de disponibilidade com base no Windows Server que usam um WSFC subjacente, o tipo de cluster padrão é WSFC e não precisa ser definido. Para grupos de disponibilidade com base em Linux, ao criar o grupo de disponibilidade, o tipo de cluster deve ser definido como Externo. A integração com o Pacemaker é configurada depois que o grupo de disponibilidade for criado, enquanto em um WSFC isso é feito no momento da criação.

Um tipo de cluster Nenhum pode ser usado com grupos de disponibilidade do Windows Server e do Linux. Definir o tipo de cluster para Nenhum significa que o grupo de disponibilidade não requer um cluster subjacente. Isso significa que o SQL Server 2017 é a primeira versão do SQL Server a dar suporte a grupos de disponibilidade sem um cluster, mas a desvantagem é que não há suporte para essa configuração como uma solução de alta disponibilidade. 

> [!IMPORTANT] 
> O SQL Server 2017 não permite a capacidade de alterar um tipo de cluster para um grupo de disponibilidade depois que ele é criado. Isso significa que um grupo de disponibilidade não pode ser alternado de Nenhum para Externo ou WSFC ou vice-versa. 

Para aqueles que estão procurando apenas adicionar outras cópias de somente leitura de um banco de dados ou como o que um grupo de disponibilidade fornece para migração/atualizações, mas não deseja que seja vinculado à complexidade adicional de um cluster subjacente ou até mesmo a replicação, um grupo de disponibilidade com um tipo de cluster Nenhum é a solução perfeita. Para obter mais informações, consulte as seções [Migrações e upgrades](#Migrations) e [Escala de leitura](#ReadScaleOut). 

A captura de tela abaixo mostra o suporte para os diferentes tipos de cluster no SSMS. Você deve estar executando a versão 17.1 ou posterior. A captura de tela abaixo é da versão 17.2.

![Opções do grupo de disponibilidade do SSMS](media/sql-server-ha-story/image2.png)
 
##### <a name="required_synchronized_secondaries_to_commit"></a>REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT

O SQL Server 2016 aumentou o suporte para o número de réplicas síncronas de duas para três na Enterprise Edition. No entanto, se uma réplica secundária foi sincronizada, mas a outra estava com problema, não havia como controlar o comportamento para informar à primária para aguardar a réplica com comportamento inadequado ou para permitir que ela prossiga. Isso significa que a réplica primária, em algum momento, continuará a receber tráfego de gravação, mesmo que a réplica secundária não esteja em um estado sincronizado, o que significa que há perda de dados na réplica secundária.
No SQL Server 2017, agora há uma opção para poder controlar o comportamento do que acontece quando há réplicas síncronas denominadas REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT. A opção funciona da seguinte maneira:
* Há três valores possíveis: 0, 1 e 2
* O valor é o número de réplicas secundárias que devem ser sincronizadas, que tem implicações para perda de dados, disponibilidade do grupo de disponibilidade e failover
* Para WSFCs e um tipo de cluster Nenhum, o valor padrão é 0 e pode ser definido manualmente como 1 ou 2
* Para um tipo de cluster Externo, por padrão, o mecanismo de cluster definirá isso e poderá ser substituído manualmente. Para três réplicas síncronas, o valor padrão será 1.
No Linux, o valor para REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT é configurado no recurso do grupo de disponibilidade no cluster. No Windows, ele é definido por meio do Transact-SQL.

Um valor maior que 0 garante maior proteção de dados, porque se o número necessário de réplicas secundárias não estiver disponível, a primária não estará disponível até que seja resolvida. REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT também afeta o comportamento de failover, pois failover automático não poderá ocorrer se o número correto de réplicas secundárias não estiver no estado apropriado. No Linux, um valor de 0 não permitirá o failover automático, então no Linux, ao usar o síncrono com o failover automático, o valor deverá ser definido como maior que 0 para alcançar o failover automático. 0 no Windows Server é o comportamento do SQL Server 2016 e anterior.

##### <a name="enhanced-microsoft-distributed-transaction-coordinator-support"></a>Suporte aprimorado ao coordenador de transações distribuídas da Microsoft

Antes do SQL Server 2016, a única maneira de obter disponibilidade no SQL Server, para aplicativos que necessitam de transações distribuídas que usam o DTC nos bastidores, era ao implantar FCIs. Uma transação distribuída pode ser feita de duas maneiras:
* Uma transação que abrange mais de um banco de dados na mesma instância do SQL Server
* Uma transação que abrange mais de uma instância do SQL Server ou possivelmente envolve uma fonte de dados que não seja do SQL Server

O SQL Server 2016 introduziu suporte parcial de DTC com grupos de disponibilidade que abordaram o último cenário. O SQL Server 2017 conclui a história ao oferecer suporte a ambos os cenários com o DTC.

Outra melhoria no suporte DTC para grupos de disponibilidade é que, no SQL Server 2016, a habilitação do suporte para DTC para um grupo de disponibilidade só poderia ser realizada quando o grupo de disponibilidade fosse criado e não poderia ser adicionada posteriormente. No SQL Server 2017, o suporte DTC também pode ser adicionado a um grupo de disponibilidade depois de ser criado.

>[!NOTE]
> O suporte DTC só pode ser configurado para bancos de dados em instâncias do SQL Server com base no Windows Server. Se o DTC for um requisito para seu aplicativo, você deverá usar o Windows Server como o sistema operacional para implantação do SQL Server e não poderá usar o Linux. 

#### <a name="always-on-failover-cluster-instances"></a>Instâncias do cluster de failover do AlwaysOn
As instalações de cluster são um recurso do SQL Server desde a versão 6.5. As FCIs são um método comprovado para fornecer disponibilidade para toda a instalação do SQL Server, conhecida como uma instância. Isso significa que tudo dentro da instância, incluindo bancos de dados, trabalhos do SQL Server Agent, servidores vinculados, entre outros, será movido para outro servidor se o servidor adjacente encontrar um problema. Todas as FCIs exigem algum tipo de armazenamento compartilhado, mesmo se ele for fornecido através da rede. Os recursos da FCI só poderão ser executados e controlados por um nó a qualquer momento. Na imagem abaixo, o primeiro nó do cluster controla a FCI, o que também significa que ele controla os recursos de armazenamento compartilhados associados a ele, indicados por uma linha sólida para o armazenamento.

![Instância de Cluster de Failover](media/sql-server-ha-story/image3.png)
 
Após um failover, a propriedade é alterada conforme a figura abaixo.

![Após o Failover](media/sql-server-ha-story/image4.png)
 
Não há perda de dados com uma FCI, mas o armazenamento compartilhado subjacente é um ponto único de falha, pois há uma cópia dos dados. As FCIs geralmente são combinadas com outro método de disponibilidade, como um grupo de disponibilidade ou o envio de logs, para ter cópias redundantes dos bancos de dados. O método adicional implantado deve usar armazenamento fisicamente separado da FCI. Quando a FCI executar o failover para outro nó, ela será interrompida em um nó e iniciará em outro, o que não é muito diferente de desligar um servidor e ligá-lo. Uma FCI passa pelo processo de recuperação normal, o que significa que todas as transações que precisam que o roll forward seja efetuado serão revertidas, assim como todas as transações que estão incompletas. Portanto, o banco de dados é consistente de um ponto de dados até o momento da falha ou do failover manual, portanto, sem perda de dados. Os bancos de dados estão disponíveis somente após a conclusão da recuperação, portanto o tempo de recuperação dependerá de muitos fatores e geralmente será maior do que a execução de um failover em um grupo de disponibilidade. A desvantagem é que, ao fazer failover em um grupo de disponibilidade, poderá haver tarefas adicionais necessárias para tornar um banco de dados utilizável, como a habilitação de uma tarefa de trabalhos do SQL Server Agent.

Como um grupo de disponibilidade, as FCIs resumem qual nó do cluster subjacente está hospedando-o. Uma FCI sempre mantém o mesmo nome. Os aplicativos e usuários finais nunca se conectam aos nós. O nome exclusivo atribuído à FCI é usado. Uma FCI pode participar de um grupo de disponibilidade como uma das instâncias que hospedam uma réplica primária ou secundária.

A lista a seguir destaca algumas diferenças de FCIs no Windows Server e no Linux:

* No Windows Server, uma FCI faz parte do processo de instalação. Uma FCI no Linux é configurada após a instalação do SQL Server.
* O Linux dá suporte a apenas uma única instalação do SQL Server por host, para que todas as FCIs sejam uma instância padrão. O Windows Server dá suporte a até 25 FCIs por WSFC.
* O nome comum usado pelas FCIs no Linux é definido no DNS e deve ser o mesmo que o recurso criado para a FCI.

#### <a name="log-shipping"></a>Envio de logs
Se os objetivos do ponto de recuperação e do tempo de recuperação forem mais flexíveis ou os bancos de dados não forem considerados altamente de missão crítica, o envio de logs será outro recurso de disponibilidade comprovado no SQL Server. Com base nos backups nativos do SQL Server, o processo de envio de logs automaticamente gera os backups de log de transações, copia-os em uma ou mais instâncias conhecidas como uma espera passiva e aplica automaticamente os backups de log de transações a esse modo de espera. O envio de logs usa trabalhos do SQL Server Agent para automatizar o processo de backup, cópia e aplicação dos backups de log de transações.

![Envio de logs](media/sql-server-ha-story/image5.png)
 
Possivelmente, a maior vantagem de usar o envio de logs, de alguma forma, é que ele é responsável por erro humano. O aplicativo dos logs de transações pode estar atrasado. Portanto, se alguém emitir algo parecido com uma ATUALIZAÇÃO sem uma cláusula WHERE, o modo em espera poderá não ter a alteração, então você poderá alternar para ela enquanto repara o sistema primário. Enquanto o envio de logs é fácil de configurar, a troca do primário para um estado de espera passiva, conhecido como uma alteração de função, é sempre manual. Uma alteração de função é iniciada por meio do Transact-SQL e, como um grupo de disponibilidade, todos os objetos não capturados no log de transações devem ser sincronizados manualmente. O envio de logs também precisa ser configurado por banco de dados, enquanto um único grupo de disponibilidade pode conter vários bancos de dados. Ao contrário de um grupo de disponibilidade ou FCI, o envio de logs não tem nenhuma abstração para uma alteração de função. Os aplicativos devem ser capazes de lidar com isso. Podem ser empregadas técnicas como um alias DNS (CNAME), mas há vantagens e desvantagens, como o tempo necessário que o DNS leva para atualizar após a troca.

## <a name="disaster-recovery"></a>Recuperação de desastre

Quando seu local de disponibilidade primária passa por um evento catastrófico, como um terremoto ou uma enchente, a empresa deve estar preparada para que seus sistemas fiquem online em outro lugar. Esta seção abordará como os recursos de disponibilidade do SQL Server podem auxiliar nessa continuidade dos negócios.

### <a name="always-on-availability-groups"></a>Grupos de disponibilidade AlwaysOn

Um dos benefícios dos grupos de disponibilidade é que a alta disponibilidade e a recuperação de desastres podem ser configuradas usando um único recurso. Sem a necessidade de garantir que o armazenamento compartilhado também é altamente disponível, é mais fácil ter réplicas que são locais em um data center para alta disponibilidade e remotas em outros dados centers para recuperação de desastres, cada uma com armazenamento separado. Ter cópias adicionais do banco de dados é a desvantagem para garantir redundância. Um exemplo de um grupo de disponibilidade que abrange vários data centers é mostrado abaixo. Uma réplica primária é responsável por manter todas as réplicas secundárias sincronizadas.

![Grupo de disponibilidade](media/sql-server-ha-story/image6.png)
 
Fora de um grupo de disponibilidade com um tipo de cluster Nenhum, um grupo de disponibilidade requer que todas as réplicas sejam parte do mesmo cluster subjacente, seja um WSFC ou Pacemaker. Isso significa que, na figura acima, o WSFC é estendido para trabalhar em dois data centers diferentes, o que adiciona complexidade. independentemente da plataforma (Windows Server ou Linux). Transferir clusters em distância adiciona complexidade. Introduzido no SQL Server 2016, um grupo de disponibilidade distribuído permite que um grupo de disponibilidade abranja grupos de disponibilidade configurados em diferentes clusters. Isso separa a necessidade de ter os nós todos participando no mesmo cluster, o que facilita a configuração de recuperação de desastres. Para obter mais informações sobre grupos de disponibilidade distribuídos, veja [Grupos de disponibilidade distribuídos](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups).

![Grupos de Disponibilidade Distribuídos](media/sql-server-ha-story/image11.png)
 
### <a name="always-on-failover-cluster-instances"></a>Instâncias do cluster de failover do AlwaysOn

As FCIs podem ser usadas para recuperação de desastres. Assim como acontece com um grupo de disponibilidade normal, o mecanismo do cluster subjacente deve ser estendido para todos os locais que adicionam complexidade. Há uma consideração adicional sobre as FCIs: o armazenamento compartilhado. Os mesmos discos precisam estar disponíveis em sites primários e secundários, então um método externo, como a funcionalidade fornecida pelo fornecedor de armazenamento na camada de hardware ou o uso da Réplica de armazenamento no Windows Server, é necessário para garantir que os discos usados pela FCI existam em outro lugar. 

![FCI do AlwaysOn](media/sql-server-ha-story/image8.png)
 
### <a name="log-shipping"></a>Envio de logs
O envio de logs é um dos métodos mais antigos para fornecer recuperação de desastres aos bancos de dados do SQL Server. O envio de logs é geralmente usado em conjunto com grupos de disponibilidade e FCIs para fornecer recuperação de desastres mais simples e econômica na qual outras opções podem ser difíceis devido ao ambiente, habilidades administrativas ou orçamento. Similar à história de alta disponibilidade para envio de logs, muitos ambientes atrasarão o carregamento de um log de transações para responsabilizar por erro humano.

## <a name = "Migrations"></a> Migrações e atualizações

Ao implantar novas instâncias ou atualizar as antigas, uma empresa não pode tolerar interrupção longa. Esta seção abordará como os recursos de disponibilidade do SQL Server podem ser usados para minimizar o tempo de inatividade em uma alteração de arquitetura planejada, troca de servidor, alteração da plataforma (como Windows Server para Linux ou vice-versa) ou durante a aplicação de patch.

> [!NOTE]
> Outros métodos, como o uso de backups e a restauração deles em outro lugar, também podem ser usados para migrações e atualizações. Eles não são abordados neste documento. 

### <a name="always-on-availability-groups"></a>Grupos de disponibilidade AlwaysOn

Uma instância existente, que contém um ou mais grupos de disponibilidade, pode ser atualizada no local para o SQL Server 2017. Enquanto isso requer algum tempo de inatividade, com a quantidade certa de planejamento, ela pode ser minimizada. 

Se a meta é migrar para novos servidores e não alterar a configuração (incluindo o sistema operacional ou a versão do SQL Server), esses servidores podem ser adicionados como nós ao cluster subjacente existente e adicionados ao grupo de disponibilidade. Depois que a réplica ou réplicas estiverem no estado correto, poderá ocorrer um failover manual para um novo servidor e, em seguida, os antigos poderão ser removidos do grupo de disponibilidade e, por fim, encerrados. 

Os grupos de disponibilidade distribuídos também são outro método para migrar para uma nova configuração ou atualizar o SQL Server. Como um grupo de disponibilidade distribuído dá suporte a diferentes grupos de disponibilidade subjacentes em arquiteturas diferentes, por exemplo, você poderá alterar do SQL Server 2016 em execução no Windows Server 2012 R2 para o SQL Server 2017 em execução no Windows Server 2016. 

![Grupo de Disponibilidade Distribuído](media/sql-server-ha-story/image10.png)

Por fim, os grupos de disponibilidade com um tipo de cluster Nenhum também podem ser usados para a migração ou atualização. Você não pode misturar e corresponder os tipos de cluster em uma configuração de grupo de disponibilidade comum, então todas as réplicas precisariam ser do tipo Nenhum. Um grupo de disponibilidade distribuído pode ser usado para estender os grupos de disponibilidade configurados com tipos de cluster diferentes. Esse método também tem suporte em todas as plataformas de sistema operacional diferentes.

Todas as variantes de grupos de disponibilidade para as migrações e atualizações permitem que a parte mais demorada do trabalho seja feita ao longo do tempo – a sincronização de dados. Quando chegar a hora de iniciar a troca para a nova configuração, a transferência será uma breve interrupção versus um longo período de tempo de inatividade em que todo o trabalho, incluindo a sincronização de dados, precisa ser concluído. 

Os grupos de disponibilidade podem fornecer o tempo de inatividade mínimo durante a aplicação de patches do sistema operacional subjacente ao fazer failover manual da réplica primária para a secundária enquanto a aplicação de patch estiver sendo concluída. Da perspectiva do sistema operacional, isso seria mais comum no Windows Server, já que frequentemente, mas nem sempre, a manutenção do sistema operacional subjacente pode exigir uma reinicialização. Às vezes, a aplicação de patch no Linux precisa de uma reinicialização, mas pode ser pouco frequente. 

[Aplicar patch nas instâncias do SQL Server que participam de um grupo de disponibilidade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances) também pode minimizar o tempo de inatividade dependendo da complexidade da arquitetura do grupo de disponibilidade. Para aplicar patch em servidores que participam de um grupo de disponibilidade, uma réplica secundária será corrigida primeiro. Depois que o número correto de réplicas for corrigido, a réplica primária terá o failover feito manualmente para outro nó a fim de fazer a atualização. Qualquer réplica secundária restante, neste ponto, também pode ser atualizada. 

### <a name="always-on-failover-cluster-instances"></a>Instâncias do cluster de failover do AlwaysOn

As FCIs sozinhas não conseguem ajudar a migração ou a atualização tradicionais. Um grupo de disponibilidade ou o envio de logs precisam ser configurados para os bancos de dados na FCI e todos os outros objetos considerados. No entanto, as FCIs no Windows Server ainda são uma opção popular para quando os Windows Servers subjacentes precisam ser corrigidos. Um failover manual pode ser iniciado, o que significa uma breve interrupção, em vez de ter a instância completamente indisponível o tempo todo em que o Windows Server está sendo corrigido.
Uma FCI pode ser atualizada no local para o SQL Server 2017. Para obter informações, consulte [Atualizar uma Instância de Cluster de Failover do SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance).

### <a name="log-shipping"></a>Envio de logs

O envio de logs ainda é uma opção popular para migrar e atualizar bancos de dados. Semelhante a grupos de disponibilidade, mas desta vez usando o log de transações como o método de sincronização, a propagação de dados pode ser iniciada antes da troca do servidor. No momento da troca, depois que todo o tráfego for interrompido na origem, um log de transações final precisará ser obtido, copiados e aplicado à nova configuração. Nesse momento, o banco de dados pode ser colocado online. O envio de logs geralmente é mais tolerante com redes mais lentas e, por mais que a troca possa ser um pouco maior do que a feita usando um grupo de disponibilidade ou um grupo de disponibilidade distribuído, ele geralmente é medido em minutos, não em horas, dias ou semanas.

Semelhante aos grupos de disponibilidade, o envio de logs pode fornecer uma maneira para alternar para outro servidor no caso de aplicação de patch.

### <a name="other-sql-server-deployment-methods-and-availability"></a>Outros métodos de implantação do SQL Server e disponibilidade

Há dois outros métodos de implantação do SQL Server no Linux: contêineres e uso do Azure (ou outro provedor de nuvem pública). A necessidade geral para disponibilidade, como apresentado neste documento, existe independentemente de como o SQL Server é implantado. Esses dois métodos têm algumas considerações especiais quando se trata de tornar o SQL Server altamente disponível.

[Contêineres usando o Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker) são uma nova maneira de implantar o SQL Server, tanto no Windows Server quanto no Linux. Um contêiner é uma imagem completa do SQL Server que está para ser executada. No entanto, no momento não há suporte nativo para o clustering e, desta forma, alta disponibilidade direta ou recuperação de desastres. No momento, as opções para disponibilizar os bancos de dados do SQL Server usando os contêineres seriam o envio de logs, backup e restauração. Enquanto um grupo de disponibilidade com um tipo de cluster Nenhum pode ser configurado, conforme observado anteriormente, ele não é considerado uma configuração de disponibilidade verdadeira. A Microsoft está analisando maneiras para habilitar grupos de disponibilidade ou FCIs usando contêineres. 

Se você estiver usando contêineres hoje, se o contêiner estiver perdido, dependendo da plataforma do contêiner, ele poderá ser implantado novamente e anexado ao armazenamento compartilhado que foi usado. Alguns desses mecanismos são fornecidos pelo orquestrador de contêiner. Enquanto isso fornece resiliência, haverá algum tempo de inatividade associado à recuperação de banco de dados e não estará realmente altamente disponível como estaria se usasse um grupo de disponibilidade ou FCI. 

As máquinas virtuais Linux IaaS podem ser implantadas com o SQL Server instalado usando o Azure. Assim como as instalações baseadas localmente, uma instalação com suporte requer o uso de STONITH (Shoot the Other Node in the Head), que é externo ao Pacemaker em si. O STONITH é fornecido por meio de agentes de disponibilidade de isolamento. Algumas distribuições os enviam como parte da plataforma, outras contam com fornecedores externos de hardware e software. Verifique sua distribuição Linux preferencial para ver quais formatos de STONITH são fornecidos para que uma solução com suporte seja implantada na nuvem pública.

## <a name="cross-platform-and-linux-distribution-interoperability"></a>Interoperabilidade de distribuição do Linux e de multiplataforma

Como o SQL Server agora tem suporte no Windows Server e Linux, esta seção aborda os cenários de como eles funcionam juntos para disponibilidade, além de outras finalidades, bem como a história para soluções que vão incorporar mais de uma distribuição do Linux.

Antes de abordar os cenários de interoperabilidade e de multiplataforma, dois fatos precisam ser declarados:

* Não há nenhum cenário no qual uma FCI com base em WSFC ou um grupo de disponibilidade funcionarão com um grupo de disponibilidade ou uma FCI com base em Linux diretamente. Um WSFC não pode ser estendido por um nó do Pacemaker e vice-versa. 
* Não há suporte para a combinação de distribuições do Linux com FCIs ou com um grupo de disponibilidade que tem um tipo de cluster Externo. Todas as réplicas do grupo de disponibilidade neste cenário devem ser configuradas não apenas com a mesma distribuição de Linux, mas também com a mesma versão. As duas formas com suporte que o SQL Server pode operar entre as duas plataformas ou várias distribuições do Linux são grupos de disponibilidade e envio de logs.

## <a name="distributed-availability-groups"></a>Grupos de disponibilidade distribuídos 

Os grupos de disponibilidade distribuídos são projetados para abranger as configurações do grupo de disponibilidade, esses dois clusters subjacentes abaixo dos grupos de disponibilidade sendo duas diferentes distribuições do Linux e de WSFCs ou uma em um WSFC e a outra no Linux. Um grupo de disponibilidade distribuído será o principal método para ter uma solução de plataforma cruzada. Um grupo de disponibilidade distribuído também é a principal solução para migrações, como converter de uma infraestrutura do SQL Server com base no Windows Server para uma com base em Linux, se isso for o que sua empresa deseja fazer. Conforme observado acima, os grupos de disponibilidade e, especialmente, os grupos de disponibilidade distribuídos, devem minimizar o tempo que um aplicativo estaria indisponível para uso. Um exemplo de um grupo de disponibilidade distribuído que abrange um WSFC e o Pacemaker é mostrado abaixo.

![Grupos de Disponibilidade Distribuídos](media/sql-server-ha-story/image9.png)
 
Se um grupo de disponibilidade estiver configurado com um tipo de cluster Nenhum, isso poderá abranger o Windows Server e o Linux, bem como várias distribuições do Linux. Como esta não é uma configuração de alta disponibilidade verdadeira, ela não deve ser usada para implantações de missão crítica, mas para cenários de escala de leitura ou migração/atualização.

## <a name="log-shipping"></a>Envio de logs

Como o envio de logs baseia-se somente no backup e na restauração, e não existem diferenças nos bancos de dados, estruturas de arquivos, entre outros, para o SQL Server no Windows Server em comparação com o SQL Server no Linux. Isso significa que o envio de logs pode ser configurado entre uma instalação do SQL Server com base no Windows Server e uma do Linux, bem como entre distribuições do Linux. Todo o resto permanece o mesmo. A única ressalva é que o envio de logs, assim como um grupo de disponibilidade, não funciona quando a fonte estiver em uma versão principal superior do SQL Server em relação a um destino que é uma versão inferior do SQL Server. 

## <a name = "ReadScaleOut"></a> Escala de leitura

Desde seu lançamento no SQL Server 2012, as réplicas secundárias tiveram a capacidade de serem usadas para consultas somente leitura. Há duas maneiras que podem ser obtidas com um grupo de disponibilidade: permitindo o acesso direto ao secundário, bem como [configurando o roteamento de somente leitura](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server), que requer o uso do ouvinte.  O SQL Server 2016 introduziu a capacidade de balancear carga de conexões de somente leitura por meio do ouvinte usando um algoritmo de round robin, permitindo que as solicitações de somente leitura sejam distribuídas em todas as réplicas legíveis. 

> [!NOTE]
> As réplicas secundárias legíveis são um recurso apenas na Enterprise Edition e cada instância que hospeda uma réplica legível precisaria de uma licença do SQL Server.

O dimensionamento de cópias legíveis de um banco de dados por meio de grupos de disponibilidade foi introduzido com grupos de disponibilidade distribuídos no SQL Server 2016. Isso permitiria que as empresas tivessem cópias de somente leitura do banco de dados não apenas localmente, mas regional e globalmente com uma quantidade mínima de configuração e reduziria o tráfego de rede e a latência ao executar as consultas localmente. Cada réplica primária de um grupo de disponibilidade pode propagar dois grupos de disponibilidade, mesmo se não for a cópia de leitura/gravação completa, então cada grupo de disponibilidade distribuído poderá oferecer suporte a até 27 cópias dos dados que podem ser lidos. 

![Grupos de Disponibilidade Distribuídos](media/sql-server-ha-story/image11.png)

Começando com o SQL Server 2017, é possível criar uma solução de somente leitura quase em tempo real com grupos de disponibilidade configurados com um tipo de cluster Nenhum. Se a meta é usar grupos de disponibilidade para réplicas secundárias legíveis e não de disponibilidade, isso elimina a complexidade do uso de um WSFC ou Pacemaker, além de oferecer os benefícios legíveis de um grupo de disponibilidade em um método de implantação mais simples. 

A única principal ressalva é que, devido a nenhum cluster subjacente com um tipo de cluster Nenhum, configurar o roteamento somente leitura é um pouco diferente. Da perspectiva do SQL Server, um ouvinte ainda é necessário para encaminhar as solicitações, embora não exista nenhum cluster. Em vez de configurar um ouvinte tradicional, o endereço IP ou o nome da réplica primária são usados. A réplica primária é, então, usada para direcionar as solicitações de somente leitura.

Uma espera passiva para envio de logs pode tecnicamente ser configurada para uso legível ao restaurar o banco de dados WITH STANDBY. No entanto, como os logs de transações exigem o uso exclusivo do banco de dados para restauração, isso significa que usuários não podem estar acessando o banco de dados enquanto isso acontece. Isso tornará o envio de logs uma solução abaixo do ideal, especialmente se os dados quase em tempo real forem necessários. 

Uma coisa que deve ser observada em todos os cenários de escala de leitura com grupos de disponibilidade é que, ao contrário de usar a replicação transacional na qual todos os dados são dinâmicos, cada réplica secundária não está em um estado no qual os índices exclusivos podem ser aplicados, a réplica é uma cópia exata da primária. Isso significa que, se todos os índices forem necessários para relatórios ou os dados precisarem ser manipulados, isso deverá ser feito em bancos de dados na réplica primária. Se você precisar dessa flexibilidade, a replicação será uma solução melhor para dados legíveis.

## <a name="summary"></a>Resumo

As instâncias e os bancos de dados do SQL Server 2017 podem se tornar altamente disponíveis usando os mesmos recursos no Windows Server e no Linux. Além de cenários de disponibilidade padrão de recuperação de desastres e alta disponibilidade local, o tempo de inatividade associado a migrações e atualizações pode ser minimizado com os recursos de disponibilidade do SQL Server. Os grupos de disponibilidade também podem fornecer cópias adicionais de um banco de dados como parte da mesma arquitetura para expandir cópias legíveis. Se você estiver implantando uma nova solução usando o SQL Server 2017 ou considerando fazer uma atualização, o SQL Server 2017 tem a disponibilidade e a confiabilidade que você precisa.
 
[SimpleAG]:media\sql-server-ha-story\image1.png
[SSMSAGOptions]:media\sql-server-ha-story\image2.png
[BasicFCI]:media\sql-server-ha-story\image3.png
[PostFailoverFCI]:media\sql-server-ha-story\image4.png
[LogShipping]:media\sql-server-ha-story\image5.png
[AG]:media\sql-server-ha-story\image6.png
[DAG]:media\sql-server-ha-story\image7.png
[AlwaysOnFCI]:media\sql-server-ha-story\image8.png
[BasicDAG]:media\sql-server-ha-story\image9.png
[image10]:media\sql-server-ha-story\image10.png
[DAG]:media\sql-server-ha-story\image11.png
