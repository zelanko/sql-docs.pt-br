---
title: "Replica&#231;&#227;o transacional ponto a ponto | Microsoft Docs"
ms.custom: ""
ms.date: "08/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicação bidirecional"
  - "replicação transacional, replicação bidirecional"
  - "replicação transacional bidirecional"
  - "replicação transacional, replicação ponto a ponto."
  - "replicação transacional ponto a ponto"
ms.assetid: 23e7e8c1-002f-4e69-8c99-d63e4100de64
caps.latest.revision: 71
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 71
---
# Replica&#231;&#227;o transacional ponto a ponto
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Replicação ponto a ponto fornece uma solução de expansão e alta disponibilidade, mantendo cópias de dados em várias instâncias de servidor, também conhecidas como *nós*. Criada na base da replicação transacional, a replicação ponto a ponto se propaga de forma transacional, de acordo com as alterações em tempo real. Ativa aplicativos que requerem operações expandidas de leitura para distribuir as leituras de clientes em vários nós. Como os dados são mantidos em todos os nós em tempo quase real, a replicação ponto a ponto fornece redundância de dados, o que amplia a disponibilidade de dados.  
  
 Considere um aplicativo da Web. Ele pode se beneficiar da replicação ponto a ponto dos seguintes modos:  
  
-   As consultas de catálogo e outras leituras são disseminadas por vários nós. Isso permite que o desempenho permaneça consistente à medida que as leituras aumentam.  
  
-   Se um dos nós do sistema falhar, uma camada de aplicativo poderá redirecionar as gravações daquele nó para outro nó. Isso mantém a disponibilidade.  
  
-   Se um nó exigir a manutenção ou o sistema inteiro necessitar de uma atualização, cada nó poderá ser posto offline e adicionado de volta ao sistema sem que a disponibilidade do aplicativo seja afetada.  
  
 Embora a replicação ponto a ponto ative a expansão das operações de leitura, o desempenho de gravação para a topologia é igual à de um único nó. Isso ocorre porque, essencialmente, todas as inserções, atualizações e exclusões são propagadas para todos os nós. A replicação reconhece quando uma alteração foi aplicada a um determinado nó e impede que as alterações sejam cíclicas nos nós, mais de uma vez. É altamente recomendado que as operações de gravação de cada linha seja realizada em único nó, pelos seguintes motivos:  
  
-   Se uma linha for modificada em mais de um nó, isso poderá causar um conflito ou mesmo uma atualização perdida quando a linha for propagada para outros nós.  
  
-   Há sempre alguma latência envolvida quando as alterações são replicadas. Com relação aos aplicativos que requerem que a última alteração seja vista de imediato, equilibrar a carga do aplicativo de maneira dinâmica pelos vários nós poderá se transformar em um problema.  
  
 A replicação ponto a ponto inclui a opção de ativar a detecção de conflito por uma topologia ponto a ponto. Essa opção ajuda a evitar os problemas causados por conflitos não detectados, inclusive o comportamento inconsistente do aplicativo e as atualizações perdidas. Ao ativar essa opção, por padrão uma alteração de conflito é tratada como erro crítico que causa a falha do Distribution Agent. No evento de um conflito, a topologia é mantida em um estado inconsistente até que o conflito seja resolvido manualmente e os dados sejam tornados consistentes em toda a topologia. Para obter mais informações, consulte [detecção de conflitos em replicação ponto a ponto](../../../relational-databases/replication/transactional/conflict-detection-in-peer-to-peer-replication.md).  
  
> [!NOTE]  
>  Para evitar inconsistência potencial de dados, certifique-se de evitar conflitos em uma topologia ponto a ponto, mesmo com a detecção de conflitos ativada. Para assegurar que as operações de gravação de uma linha particular sejam realizadas em um único nó, os aplicativos que acessam e alteram dados devem realizar operações de partição, inserção, atualização e exclusão. Esse particionamento assegurará que as modificações de uma determinada linha originária de um nó sejam sincronizadas com todos os outros nós da topologia antes que a linha seja modificada por um outro nó. Se um aplicativo requerer detecção de conflito e recursos de resolução sofisticados, use a replicação de mesclagem. Para obter mais informações, consulte [replicação de mesclagem](../../../relational-databases/replication/merge/merge-replication.md) e [detectar e resolver conflitos de replicação de mesclagem](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md).  
  
## Topologias ponto a ponto  
 Os cenários a seguir ilustram usos típicos para replicação ponto a ponto.  
  
### Topologia com participação de dois bancos de dados  
 ![Replicação ponto a ponto, dois nós](../../../relational-databases/replication/transactional/media/repl-multinode-01.gif "Replicação ponto a ponto, dois nós")  
  
 Ambas as ilustrações precedentes mostram dois bancos de dados participantes, com tráfego de usuário direcionado para os bancos de dados por meio do servidor de aplicativos. Essa configuração pode ser usada para uma série de aplicativos, de sites a aplicativos de grupos de trabalho, e oferece as seguintes vantagens:  
  
-   Desempenho melhorado de leitura, porque as leituras são difundidas em mais de dois servidores.  
  
-   Disponibilidade superior, caso a manutenção seja necessária ou em caso de falha de um nó.  
  
 Em ambas as ilustrações, a atividade de leitura é equilibrada por carga entre os bancos de dados participantes, mas as atualizações são controladas diferentemente:  
  
-   À esquerda, as atualizações são particionadas entre os dois servidores. Se o banco de dados contiver um catálogo de produtos, você poderá, por exemplo, fazer com que um aplicativo personalizado atualize diretamente no nó **A** com relação aos nomes de produto começando de A a M, e que ele atualize diretamente no nó **B** com relação aos nomes de produtos começando de N a Z. As atualizações, em seguida, são replicadas no outro nó.  
  
-   À direita, todas as atualizações são direcionadas ao nó **B**. A partir daí, as atualizações são replicadas para o nó **A**. Se **B** estiver offline (por exemplo, para manutenção), o servidor de aplicativos pode direcionar todas as atividades para **um**. Quando **B** está on-line novamente, as atualizações poderão fluir para ele e o servidor de aplicativos pode mover todas as atualizações de volta para **B** ou continuar a direcioná-los para **um**.  
  
 A replicação ponto a ponto pode oferecer suporte a ambas as abordagens, mas o exemplo de atualização central à direita é também usado com frequência na replicação transacional padrão.  
  
### Topologias com três ou mais bancos de dados participantes  
 ![Replicação ponto a ponto para locais dispersos](../../../relational-databases/replication/transactional/media/repl-multinode-02.gif "Replicação ponto a ponto para locais dispersos")  
  
 A ilustração anterior mostra três bancos de dados participantes que fornecem dados para uma organização de suporte a software mundial, e com escritórios em Los Angeles, Londres e Taipei. Os engenheiros de suporte de cada escritório recebem chamadas telefônicas e atualizam informações sobre cada uma das chamadas de cliente. Os fusos horários dos três escritórios têm oito horas de diferença entre si, de modo a não haver sobreposições no dia de trabalho. O escritório de Taipei fecha, quando o escritório de Londres está apenas começando o expediente. Se uma chamada ainda está em andamento quando um escritório estiver fechando, a chamada será transferida para um representante no primeiro escritório que abrir.  
  
 Cada local tem um banco de dados e um servidor de aplicativo, que são usados por engenheiros de suporte à medida que eles digitam e atualizam informações sobre as chamadas de cliente. A topologia é particionada por tempo. Por isso, as atualizações ocorrem apenas no nó que está atualmente aberto para negócios e, em seguida, elas fluem para outros bancos de dados participantes. Essa topologia oferece as seguintes vantagens:  
  
-   Independência sem isolamento: cada escritório pode inserir, atualizar ou excluir dados, de forma independente, mas também compartilhá-los, porque eles são replicados em todos os outros bancos de dados.  
  
-   Disponibilidade superior no caso de falha ou permissão de manutenção em um ou mais dos bancos de dados participantes.  
  
     ![Replicação ponto a ponto, três e quatro nós](../../../relational-databases/replication/transactional/media/repl-multinode-04.gif "Replicação ponto a ponto, três e quatro nós")  
  
 A ilustração anterior mostra a adição de um nó à topologia de três nós. Um nó poderia ser adicionado a esse cenário pelos seguintes motivos:  
  
-   Porque outro escritório foi aberto.  
  
-   Para fornecer alta disponibilidade em suporte à manutenção ou para aumentar a tolerância a falhas, ou caso ocorra uma falha de disco ou outra falha significativa.  
  
 Observe que nas topologias de três ou quatro nós, todos os bancos de dados publicam e assinam todos os outros bancos de dados. Isso oferece um máximo de disponibilidade no caso de necessidades de manutenção ou falha de um ou mais nós. À medida que os nós são adicionados, é preciso equilibrar as necessidades de disponibilidade e escalabilidade, segundo o desempenho e a complexidade da implantação e do gerenciamento.  
  
## Configurando a replicação ponto a ponto  
 Configurar uma topologia de replicação ponto a ponto é bem semelhante a configurar uma série de publicações transacionais e assinaturas padrão. As etapas descritas nos tópicos a seguir mostram a configuração de um sistema de três nós, semelhante à configuração mostrada à esquerda da ilustração anterior, que apresenta a topologia ponto a ponto.  
  
## Considerações sobre o uso da replicação ponto a ponto  
 Esta seção fornece informações e diretrizes para avaliar o momento a usar a replicação ponto a ponto.  
  
### Considerações gerais  
  
-   A replicação ponto a ponto está disponível somente em versões Enterprise do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Todos os bancos de dados que participam da replicação ponto a ponto devem conter esquema e dados idênticos:  
  
    -   Os nomes de objeto, de esquema de objeto e de publicação devem ser idênticos.  
  
    -   As publicações precisam permitir a replicação de alterações de esquema. (Essa é uma configuração de **1** para a propriedade de publicação **replicate_ddl**, que é a configuração padrão.) Para obter mais informações, consulte [fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
    -   Não há suporte para filtragens de linha e de coluna.  
  
-   Recomenda-se que cada nó use o seu próprio banco de dados de distribuição. Isso elimina o potencial de haver um único ponto de falha.  
  
-   Tabelas e outros objetos não podem ser incluídos em várias publicações ponto a ponto em um único banco de dados de publicação.  
  
-   Uma publicação precisa ser ativada para replicação ponto a ponto antes que qualquer assinatura seja criada.  
  
-   As assinaturas devem ser inicializadas usando-se um backup ou com a opção **'suporte para replicação somente'** . Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
-   O uso de colunas de identidade não é recomendado. Ao usar identidades, será preciso gerenciar manualmente os intervalos atribuídos às tabelas em todos os bancos de dados participantes. Para obter mais informações, consulte a seção "Atribuindo intervalos para Manual gerenciamento intervalo de identidade" em [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### Restrições de recursos  
 A replicação ponto a ponto oferece suporte aos principais recursos da replicação transacional, mas não às seguintes opções:  
  
-   Inicialização e reinicialização com um instantâneo.  
  
-   Filtros de linha e de coluna.  
  
-   Colunas de carimbo de data/hora.  
  
-   Publicadores e Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Assinaturas de atualização imediata e de atualização em fila.  
  
-   Assinaturas anônimas.  
  
-   Assinaturas parciais.  
  
-   Assinaturas anexáveis e assinaturas transformáveis. (Essas duas opções foram preteridas no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].)  
  
-   Distribution Agents compartilhados.  
  
-   O parâmetro do agente de distribuição **- SubscriptionStreams** e o parâmetro Log Reader Agent **- MaxCmdsInTran**.  
  
-   As propriedades do artigo **@destination_owner** e **@destination_table**.

-   Replicação transacional ponto a ponto não oferece suporte à criação de uma assinatura transacional unidirecional em uma publicação ponto a ponto   
  
 As propriedades a seguir têm considerações especiais:  
  
-   A propriedade de publicação **@allow_initialize_from_backup** requer um valor de **true**.  
  
-   A propriedade de artigo **@replicate_ddl** requer um valor de **true**; **@identityrangemanagementoption** requer um valor de **manual**; e **@status** requer que a opção **24** está definido.  
  
-   O valor de propriedades do artigo **@ins_cmd**, **@del_cmd**, e **@upd_cmd** não pode ser definida como **SQL**.  
  
-   A propriedade de assinatura **@sync_type** requer um valor de **nenhum** ou **automáticas**.  
  
### Considerações sobre manutenção  
 Algumas ações exigem que o sistema esteja inativo. Isso significa parar as atividades em tabelas publicadas em todos os nós e assegurar que todos os nós tenham recebido todas as alterações de todos os outros nós.  
  
||Somente pares do SQL Server 2005 ou combinação de pares do SQL Server 2005 com o SQL Server 2008 e superior|Somente pares do SQL Server 2005 ou combinação de pares do SQL Server 2005 com o SQL Server 2008 e superior|Pares do SQL2008 e superior|Pares do SQL2008 e superior|  
|-|------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|------------------------------|------------------------------|  
|Adicionando um nó à topologia|2 nós na topologia completa: sem pausas necessárias. Use `sync_type = 'initialize with backup'`.|Mais de 2 nós: pausas necessárias.|`sync_type = 'replication support only'`: pausas necessárias.|`sync_type = 'initialize with backup'` e `'initialize from lsn'`: sem pausas necessárias.|  
  
 As alterações do esquema de topologia (adicionar ou remover um artigo) precisam ser desativadas. Para obter mais informações, consulte [administrar uma topologia ponto a ponto e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md).  
  
 A remoção de um nó da topologia nunca requer desativação.  
  
 Alterar as propriedades do artigo usando  [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) Nunca exigir a desativação. Alterações permitidas (de P2P) são o `description`, `ins_cmd`, `upd_cmd`, e `del_cmd` Propriedades.  
  
 As alterações de Esquema de Artigo (adicionar/remover coluna) nunca requerem desativação.  
  
-   Adicionar artigo: para adicionar um artigo a uma configuração existente, é necessário desativar o sistema, executar a instrução CREATE TABLE e carregar os dados iniciais em cada nó na topologia e adicionar o novo artigo em cada nó na topologia.  
  
-   Removendo um artigo: se quisermos um estado consistente em todos os nós, precisamos confirmar a topologia  
  
 Para obter mais informações, consulte [Confirmar uma topologia de replicação e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md) e [administrar uma topologia ponto a ponto e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md).  
  
-   Se você adicionar um novo nó em uma topologia ponto a ponto, você deve restaurar apenas dos backups criados após o novo nó foi adicionado.  
  
-   Você não pode reinicializar assinaturas em uma topologia ponto a ponto. Se for necessário garantir que um nó tenha uma nova cópia dos dados, restaure o backup no nó.  
  
## Consulte também  
 [Administrar uma topologia ponto a ponto e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)   
 [Tipos de publicação para Replicação Transacional](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)  
  
  