---
title: "Perguntas frequentes para os administradores de replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "administrando a replicação, perguntas frequentes"
  - "replicação [SQL Server], administrando"
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# Perguntas frequentes para os administradores de replica&#231;&#227;o
  As perguntas e as respostas a seguir fornecem orientação sobre várias tarefas enfrentadas pelos administradores de bancos de dados replicados.  
  
## Configurando a replicação.  
  
### A atividade precisa ser interrompida em um banco de dados quando é publicada?  
 Nenhum. A atividade pode continuar no banco de dados enquanto a publicação está sendo criada. Esteja ciente de que a produção de um instantâneo pode usar muitos recursos, portanto é melhor gerar instantâneos durante o período de pouca atividade no banco de dados (por padrão, um instantâneo é gerado quando o Assistente para Nova Publicação é concluído).  
  
### As tabelas são bloqueadas durante a geração de instantâneos?  
 O tempo dos bloqueios efetuados depende do tipo de replicação usado:  
  
-   Para as publicações de mesclagem, o Snapshot Agent não requer nenhum bloqueio.  
  
-   Para publicações transacionais, por padrão, o Agente de Instantâneo é bloqueado somente durante a fase inicial da geração de instantâneos.  
  
-   Para publicações de instantâneos, o Agente de Instantâneo não é bloqueado durante todo o processo de geração de instantâneos.  
  
 Como os bloqueios impedem que outros usuários atualizem as tabelas, o Agente de Instantâneo deverá ser programado para executar durante os períodos de pouca atividade, especialmente para as publicações de instantâneos.  
  
### Quando uma assinatura estará disponível e quando o banco de dados de assinatura poderá ser usado?  
 Uma assinatura está disponível após o instantâneo ter sido aplicado ao banco de dados de assinatura. Apesar do banco de dados de assinatura estar acessível antes disso, o banco de dados não deve ser utilizado até o instantâneo ter sido aplicado. Use o Replication Monitor para verificar o estado da geração e a aplicação do instantâneo:  
  
-   O instantâneo é gerado pelo Agente de Instantâneo. Exiba o estado da geração do instantâneo na guia **Agentes** para uma publicação no Replication Monitor. Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   O instantâneo é aplicado pelo Agente de Distribuição ou pelo Agente de Mesclagem. Exiba o estado da aplicação do instantâneo na página **Agente de Distribuição** ou **Agente de Mesclagem** do Replication Monitor. Para obter mais informações, consulte [Exibir informações e executar tarefas para os agentes associados a uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
### O que acontece se o Agente de Instantâneo não concluir quando os Distribution ou Agente de Mesclagem são iniciados?  
 Nenhum erro ocorrerá se o Agente de Distribuição ou o Agente de Mesclagem executarem ao mesmo tempo em que o Agente de Instantâneo. Porém, você deve estar atento quanto ao seguinte:  
  
-   Se o Agente de Distribuição ou o Agente de Mesclagem estiverem configurados para executar de modo contínuo, o agente aplica o instantâneo automaticamente, após a conclusão do Agente de Instantâneo.  
  
-   Se o Agente de Distribuição ou o Agente de Mesclagem estiverem configurados para executar em uma programação ou sob demanda, e não há instantâneos disponíveis quando o agente for executar, o agente será fechado exibindo uma mensagem indicando que o instantâneo não está disponível. Você deverá executar o agente novamente para aplicar o instantâneo após o Agente de Instantâneo ter concluído. Para obter mais informações sobre a execução de agentes, consulte [sincronizar uma assinatura Push](../../../relational-databases/replication/synchronize-a-push-subscription.md), [sincronizar uma assinatura Pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md), e [conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
### Devo efetuar o script de minha configuração de replicação?  
 Sim. A realização do script da configuração da replicação é peça fundamental em qualquer plano de recuperação de desastres abrangendo uma topologia de replicação. Para obter mais informações sobre a realização de script, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
### Que modelo de recuperação é requerido em um banco de dados replicado?  
 A replicação funciona corretamente seja qual for modelo de recuperação usado: simples, registrado em massa ou completo. A replicação de mesclagem rastreia a alteração armazenando as informações em tabelas de metadados. A replicação transacional rastreia as alterações marcando o log da transação, mas esse processo de marcação não é afetado pelo modelo de recuperação.  
  
### Por que a replicação adiciona uma coluna às tabelas replicadas, essa coluna será removida se a tabela não for publicada?  
 Para rastrear as alterações, a replicação de mesclagem e a replicação transacional, com assinaturas de atualização em fila, devem poder identificar exclusivamente cada linha em cada tabela publicada. Para realizar isso:  
  
-   Replicação de mesclagem adiciona a coluna **rowguid** a cada tabela, a menos que a tabela já tiver uma coluna de tipo de dados **uniqueidentifier** com o **ROWGUIDCOL** propriedade definida (neste caso esta coluna é usada). Se a tabela for descartada da publicação, a coluna **rowguid** será removida; mas, se uma coluna existente foi usada para o rastreamento, ela não será removida.  
  
-   Se uma publicação transacional oferece suporte a assinaturas de atualização enfileirada, a replicação adiciona a coluna **msrepl_tran_version** para cada tabela. Se a tabela for descartada da publicação, o **msrepl_tran_version** coluna não é removida.  
  
-   Um filtro não deve incluir o **rowguidcol** usado por replicação para identificar linhas. Por padrão, esta é a coluna adicionada no momento que você define a replicação de mesclagem e é denominada **rowguid**.  
  
### Como administrar as restrições em tabelas publicadas?  
 Há vários assuntos para serem considerados com relação à restrições em tabelas publicadas:  
  
-   A replicação transacional requer uma restrição de chave primária em cada tabela publicada. A replicação de mesclagem não requer nenhuma chave primária, mas se houver uma, ela deverá ser replicada. A replicação de instantâneos não requer nenhuma chave primária.  
  
-   Por padrão, as restrições de chave primária, os índices e as restrições de verificações são replicados nos Assinantes.  
  
-   A opção NOT FOR REPLICATION é especificada por padrão para as restrições de chave estrangeira e para as restrições de verificação; as restrições são impostas para operações de usuários mas não operações de agentes.  
  
 Para obter informações sobre como definir as opções de esquema que controlam se as restrições são replicadas, consulte [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
### Como gerenciar as colunas de identidade?  
 A replicação fornece um gerenciamento automático do intervalo de identidade para as topologias de replicação que incluem atualizações no Assinante. Para obter mais informações, consulte [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### Os mesmos objetos podem ser publicados em publicações diferentes?  
 Sim, mas com algumas restrições. Para obter mais informações, consulte a seção "Publicando tabelas em mais de uma publicação" no tópico [publica dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
### Várias publicações podem usar o mesmo banco de dados de distribuição?  
 Sim. Não há nenhuma restrição sobre o número ou tipos de publicações que podem usar o mesmo banco de dados de distribuição. Todas as publicações de um determinado Publicador devem usar o mesmo Distribuidor e o mesmo banco de dados de distribuição.  
  
 Se há várias publicações, você pode configurar vários bancos de dados de distribuição no Distribuidor para certificar-se de que os dados fluindo em cada banco de dados de distribuição sejam de uma única publicação. Use o **Propriedades do distribuidor** caixa de diálogo ou [sp_adddistributiondb & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) Para adicionar um banco de dados de distribuição. Para obter mais informações sobre como acessar a caixa de diálogo, consulte [Exibir e modificar o distribuidor e propriedades do publicador](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### Como posso localizar as informações sobre o Distribuidor e o Publicador, tal como os objetos em um banco de dados que podem ser publicados?  
 Essas informações estão disponíveis por meio do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e dos vários procedimentos de replicação armazenados. Para obter mais informações, consulte [Distributor and Publisher Information Script](../../../relational-databases/replication/administration/distributor-and-publisher-information-script.md).  
  
### A replicação criptografa dados?  
 Nenhum. A replicação não criptografa dados armazenados no banco de dados nem transferidos pela rede. Para obter mais informações, consulte a seção "Criptografia" do tópico [Visão geral de segurança e 40; Replicação e 41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
### Como posso replicar dados pela Internet?  
 Replique os dados pela Internet, por meio de:  
  
-   Uma VPN (Virtual Private Network). Para obter mais informações, consulte [publicar dados pela Internet usando VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
-   Opção de sincronização da Web para replicação de mesclagem. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Todos os tipos de replicação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem replicar dados por uma VPN, no entanto, recomenda-se a sincronização da Web quando a replicação de mesclagem for utilizada.  
  
### A replicação será retomada se uma conexão for cancelada  
 Sim. O processamento de replicação é retomado no ponto em que ele foi interrompido quando a conexão foi cancelada. Se estiver usando uma replicação de mesclagem em uma rede não confiável, tente usar os registros lógicos, isto garantirá que as alterações sejam processadas como uma unidade. Para obter mais informações, consulte [grupo alterações nas linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
### A replicação trabalha em conexões de largura de banda baixa? Ela usa a compressão?  
 Sim, a replicação trabalha em conexões de largura de banda baixa Para conexões em TCP/IP, ela usa a compressão fornecida pelo protocolo, mas não fornece nenhuma compressão adicional. Em conexões de sincronização da Web em HTTPS, ela usa a compressão fornecida pelo protocolo e também a compressão adicional dos arquivos XML usados para replicar as alterações.  
  
## Propriedade de logons e de objetos  
  
### Os logons e as senhas são replicados?  
 Nenhum. Você pode criar um pacote DTS para transferir os logons e as senhas do Publicador para um ou mais Assinantes.  
  
### O que são os esquemas e como eles são replicados?  
 A começar pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *esquema* tem dois significados:  
  
-   A definição de um objeto, como uma instrução CREATE TABLE. Por padrão, a replicação copia as definições de todos os objetos replicados para o Assinante.  
  
-   O namespace no qual um objeto é criado: \< banco de dados>. \< esquema>. \< objeto>. Os esquemas são definidos usando a instrução CREATE SCHEMA.  
  
-   A replicação tem o seguinte comportamento padrão no Assistente para Nova Publicação em relação à propriedade de esquemas e objetos:  
  
-   Para artigos em publicações de mesclagem com um nível de compatibilidade 90 ou superior, publicações de instantâneos e publicações transacionais: por padrão, o proprietário do objeto no Assinante é igual ao proprietário do objeto correspondente no Publicador. Caso não existam esquemas proprietários de objetos no Assinante, eles serão criados automaticamente.  
  
-   Para artigos em publicação de mesclagem com um nível de compatibilidade abaixo de 90: por padrão, o proprietário é deixado em branco e especificado como **dbo** durante a criação do objeto no Assinante.  
  
-   Para artigos em publicações Oracle: por padrão, o proprietário é especificado como **dbo**.  
  
-   Para artigos em publicações que usam instantâneos de modo de caracteres (que são usados para Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Assinantes [!INCLUDE[ssEW](../../../includes/ssew-md.md)]): por padrão o proprietário é deixado em branco. O proprietário assume o padrão do proprietário associado à conta usada pelo Agente de Distribuição ou Agente de Mesclagem para se conectar ao Assinante.  
  
 O proprietário do objeto pode ser alterado por meio de **Propriedades de artigo - \<***artigo***>** caixa de diálogo e por meio dos seguintes procedimentos armazenados: **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle**, e **sp_changemergearticle**. Para obter mais informações, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md), e [Exibir e modificar propriedades de artigo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### Como as concessões no banco de dados de assinatura podem ser configuradas para corresponder às concessões no banco de dados de publicação?  
 Por padrão, a replicação não executa instruções GRANT no banco de dados de assinatura. Se quiser que as permissões no banco de dados de assinatura correspondam àquelas no banco de dados de publicação, use um dos seguintes métodos:  
  
-   Execute as instruções GRANT diretamente no banco de dados de assinatura.  
  
-   Use um script de pós-instantâneo para executar as instruções. Para obter mais informações, consulte [Executar Scripts antes e após a aplicação do instantâneo](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Use o procedimento armazenado [sp_addscriptexec](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) para executar as instruções.  
  
### O que acontece às permissões concedidas em um banco de dados de assinatura se uma assinatura for reinicializada?  
 Por padrão, os objetos no Assinante são cancelados e criados novamente quando uma assinatura é reinicializada, isto que faz com que todas as permissões concedidas para aqueles objetos sejam canceladas. Há dois modos para controlar isto:  
  
-   Aplique novamente as concessões após a reinicialização, usando as técnicas descritas na seção anterior.  
  
-   Especifique que os objetos não devem ser descartados quando a assinatura for reinicializada. Antes da reinicialização, você deve:  
  
    -   Executar [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) ou [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de 'pre_creation_cmd' (**sp_changearticle**) ou 'pre_creation_command' (**sp_changemergearticle**) para o parâmetro **@property** e um valor de 'none', 'delete' ou 'Truncar' para o parâmetro **@value**.  
  
    -   No **Propriedades do artigo - \< artigo>** da caixa de diálogo de **o objeto de destino** seção, selecione um valor de **Manter objeto existente inalterado**, **Excluir dados. Se o artigo tiver um filtro de linha, exclua somente os dados que corresponde ao filtro.** ou **Truncar todos os dados no objeto existente** fou the option **Ação se o nome estiver em uso**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## Manutenção do banco de dados  
  
### Por que não consigo executar TRUNCATE TABLE em uma tabela publicada?  
 TRUNCATE TABLE é uma operação não registrada que não ativa os gatilhos. Isso não é permitido, pois a replicação não pode rastrear as alterações causadas pela operação: a replicação transacional rastreia as alterações por meio do log de transações; a replicação de mesclagem rastreia as alterações por meio de gatilhos, nas tabelas publicadas.  
  
### Qual é o efeito de se executar um comando de inserção em massa em um banco de dados replicado?  
 Para a replicação transacional, as inserções em massa são rastreadas e replicadas como as demais inserções. Para a replicação de mesclagem, você deve certificar-se de que os metadados de rastreamento de alterações estejam corretamente atualizados.  
  
### Existem algumas considerações para o backup e a restauração?  
 Sim. Existem várias considerações especiais para os bancos de dados envolvidos em replicação. Para obter mais informações, consulte [fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
### A replicação afeta o tamanho do log de transações?  
 A replicação de mesclagem e a replicação de instantâneos não afetam o tamanho do log de transações, mas uma replicação transacional sim. Se um banco de dados incluir uma ou mais publicações transacionais, o log não será truncado até que todas as transações pertinentes para as publicações sejam enviadas ao banco de dados de distribuição. Se o log de transações aumentar demasiadamente, e o Agente de Leitor de Log estiver em execução com agendamento definido, considere encurtar o intervalo entre as execuções. Ou, defina-o para executar em modo contínuo. Se ele for definido para executar em modo contínuo (o padrão), garanta que ele esteja em execução. Para obter mais informações sobre como verificar o status do Log Reader Agent, consulte [Exibir informações e executar tarefas para os agentes associados com uma publicação e 40; Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
 Além disso, se você tiver definido a opção 'sync with backup' no banco de dados de publicação ou no banco de dados de distribuição, o log de transações não será truncado até o backup de todas as transações ser feito. Se o log de transações crescer demasiadamente, e você tiver essa opção definida, considere encurtar o intervalo entre os backups do log de transações. Para obter mais informações sobre backup e restauração de bancos de dados envolvidos na replicação transacional, consulte [estratégias de backup e restauração de instantâneo e replicação transacional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### Como posso reconstruir índices ou tabelas em bancos de dados replicados?  
 Há vários mecanismos para reconstruir índices. Todos podem ser usados sem considerações especiais para a replicação, exceto pelo seguinte: as chaves primárias são necessárias para as tabelas em publicações transacionais, portanto você não pode cancelar e recriar chaves primárias nessas tabelas.  
  
### Como posso adicionar ou alterar índices em bancos de dados de publicação e de assinatura?  
 Índices podem ser adicionados no Publicador ou nos Assinantes sem considerações especiais para a replicação (lembre-se de que os índices podem afetar o desempenho). CREATE INDEX e ALTER INDEX não são replicados, portanto, ao adicionar ou alterar um índice no Publicador, por exemplo, deve-se fazer a mesma adição ou alteração no Assinante para que ele esteja refletido lá.  
  
### Como posso mover ou renomear arquivos para bancos de dados envolvidos em replicação?  
 Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], para mover ou renomear arquivos de banco de dados era necessário desanexar e tornar a anexar o banco de dados. Como um banco de dados replicado não pode ser desanexado, a replicação devia ser removida antes que os bancos de dados. A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], é possível mover ou renomear arquivos sem desanexar e anexar novamente o banco de dados, e não produzir efeito sobre a replicação. Para obter mais informações sobre como mover e renomear arquivos, consulte [ALTER DATABASE & #40. O Transact-SQL e 41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
### Como posso descartar uma tabela que está sendo replicada?  
 Primeiro descarte o artigo da publicação usando [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md), ou o **Propriedades de publicação - \< publicação>** caixa de diálogo caixa e, em seguida, solte-o do banco de dados usando `DROP <Object>`. Não é possível descartar artigos de publicações transacionais ou de instantâneos após as assinaturas terem sido adicionadas; antes é preciso descartar as assinaturas. Para obter mais informações, consulte [Adicionar e descartar artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Como posso adicionar ou descartar colunas em uma tabela publicada?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a uma grande variedade de alterações de esquema em objetos publicados, inclusive a adição e o descarte de colunas. Por exemplo, execute ALTER TABLE... DROP COLUMN no Publicador e a instrução será replicada para os Assinantes, em seguida, será executada para descartar a coluna. Os assinantes que executam versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] suporte à adição ou descarte de colunas por meio dos procedimentos armazenados [sp_repladdcolumn](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) e [sp_repldropcolumn](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md). Para obter mais informações, consulte [fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Manutenção da Replicação  
  
### Como posso determinar se os dados no Assinante estão sincronizados com os dados no Publicador?  
 Use a validação. A validação informa se um determinado Assinante está sincronizado com o Publicador. Para obter mais informações, consulte [Validar dados replicados](../../../relational-databases/replication/validate-replicated-data.md). A validação não fornece qualquer informação sobre possíveis linhas sincronizadas incorretamente, mas a [utilidade tablediff](../../../tools/tablediff-utility.md) faz isso.  
  
### Como posso adicionar uma tabela a uma publicação existente?  
 Não é necessário interromper a atividade no banco de dados de publicação ou de assinatura para adicionar uma tabela (ou qualquer outro objeto). Adicionar uma tabela em uma publicação por meio de **Propriedades de publicação - \< publicação>** caixa de diálogo ou os procedimentos armazenados [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Para obter mais informações, consulte [Adicionar e descartar artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Como posso remover uma tabela de uma publicação?  
 Remover uma tabela da publicação usando [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md), ou o **Propriedades de publicação - \< publicação>** caixa de diálogo. Não é possível descartar artigos de publicações transacionais ou de instantâneos após as assinaturas terem sido adicionadas; antes é preciso descartar as assinaturas. Para obter mais informações, consulte [Adicionar e descartar artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Que ações exigem que as assinaturas sejam reinicializadas?  
 Há várias alterações em artigos e publicações que exigem a reinicialização das assinaturas. Para obter mais informações, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### Que ações fazem com que os instantâneos sejam invalidados?  
 Há várias alterações em artigos e publicações que invalidam os instantâneos e exigem a geração de um novo instantâneo. Para obter mais informações, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### Como posso remover a replicação?  
 As ações necessárias à remoção de replicação de banco de dados dependem se o banco de dados foi usado como um banco de dados de publicação, banco de dados de assinatura ou ambos.  
  
### Como posso determinar se há transações ou linhas a serem replicadas?  
 Para a replicação transacional, use os procedimentos armazenados ou a guia **Comandos não Distribuídos** no Replication Monitor. Para obter mais informações, consulte [comandos replicados e outras informações no banco de dados de distribuição & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
 Para replicação de mesclagem, use o procedimento armazenado **sp_showpendingchanges**. Para obter mais informações, consulte [sp_showpendingchanges & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md).  
  
### O Agente de Distribuição está muito lento? Devo reinicializar?  
 Use o **sp_replmonitorsubscriptionpendingcmds** procedimento armazenado ou o **comandos não distribuídos** guia no Replication Monitor. O procedimento armazenado e a guia exibem:  
  
-   O número de comandos no banco de dados de distribuição que não foram entregues ao Assinante selecionado. Um comando consiste em uma instrução DML (linguagem de manipulação de dados) ou uma instrução DDL (linguagem de definição de dados) Transact-SQL.  
  
-   A quantidade de tempo estimada para entrega de comandos ao Assinante. Se esse valor for maior do que a quantidade de tempo requerida para gerar e aplicar um instantâneo ao Assinante, considere reiniciar o Assinante. Para obter mais informações, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
 Para obter mais informações, consulte [sp_replmonitorsubscriptionpendingcmds & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md) e [Exibir informações e executar tarefas para os agentes associados com uma assinatura & #40. Monitor de replicação e 41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Replicação e demais recursos dos Bancos de Dados  
  
### A replicação trabalha junto com o envio de logs e espelhamento de banco de dados?  
 Sim. Para obter mais informações, consulte [replicação e envio de logs e 40; SQL Server & 41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) e [o espelhamento de banco de dados, replicação e 40; SQL Server & 41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
### A replicação trabalha junto com o uso de cluster?  
 Sim. Nenhuma consideração especial é exigida porque todos os dados são armazenados em um conjunto de discos no cluster.  
  
## Consulte também  
 [Administração e 40; Replicação e 41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Práticas recomendadas para administração de replicação](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  