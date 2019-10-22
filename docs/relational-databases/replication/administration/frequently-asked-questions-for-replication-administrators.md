---
title: Perguntas frequentes para os administradores de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, frequently asked questions
- replication [SQL Server], administering
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7ff8009136f95247bc13c213d9b656abfab28ae0
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041202"
---
# <a name="frequently-asked-questions-for-replication-administrators"></a>Perguntas frequentes para os administradores de replicação
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  As perguntas e as respostas a seguir fornecem orientação sobre várias tarefas enfrentadas pelos administradores de bancos de dados replicados.  
  
## <a name="configuring-replication"></a>Configurando a replicação.  
  
### <a name="does-activity-need-to-be-stopped-on-a-database-when-it-is-published"></a>A atividade precisa ser interrompida em um banco de dados quando é publicada?  
 Nenhum. A atividade pode continuar no banco de dados enquanto a publicação está sendo criada. Esteja ciente de que a produção de um instantâneo pode usar muitos recursos, portanto é melhor gerar instantâneos durante o período de pouca atividade no banco de dados (por padrão, um instantâneo é gerado quando o Assistente para Nova Publicação é concluído).  
  
### <a name="are-tables-locked-during-snapshot-generation"></a>As tabelas são bloqueadas durante a geração de instantâneos?  
 O tempo dos bloqueios efetuados depende do tipo de replicação usado:  
  
-   Para as publicações de mesclagem, o Snapshot Agent não requer nenhum bloqueio.  
  
-   Para publicações transacionais, por padrão, o Agente de Instantâneo é bloqueado somente durante a fase inicial da geração de instantâneos.  
  
-   Para publicações de instantâneos, o Agente de Instantâneo não é bloqueado durante todo o processo de geração de instantâneos.  
  
 Como os bloqueios impedem que outros usuários atualizem as tabelas, o Agente de Instantâneo deverá ser programado para executar durante os períodos de pouca atividade, especialmente para as publicações de instantâneos.  
  
### <a name="when-is-a-subscription-available-when-can-the-subscription-database-be-used"></a>Quando uma assinatura estará disponível e quando o banco de dados de assinatura poderá ser usado?  
 Uma assinatura está disponível após o instantâneo ter sido aplicado ao banco de dados de assinatura. Apesar do banco de dados de assinatura estar acessível antes disso, o banco de dados não deve ser utilizado até o instantâneo ter sido aplicado. Use o Replication Monitor para verificar o estado da geração e a aplicação do instantâneo:  
  
-   O instantâneo é gerado pelo Agente de Instantâneo. Exiba o estado da geração do instantâneo na guia **Agentes** para uma publicação no Replication Monitor. Para obter mais informações, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   O instantâneo é aplicado pelo Agente de Distribuição ou pelo Agente de Mesclagem. Exiba o estado da aplicação do instantâneo na página **Agente de Distribuição** ou **Agente de Mesclagem** do Replication Monitor. Para obter mais informações, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
### <a name="what-happens-if-the-snapshot-agent-has-not-completed-when-the-distribution-or-merge-agent-starts"></a>O que acontece se o Agente de Instantâneo não concluir quando os Distribution ou Agente de Mesclagem são iniciados?  
 Nenhum erro ocorrerá se o Agente de Distribuição ou o Agente de Mesclagem executarem ao mesmo tempo em que o Agente de Instantâneo. Porém, você deve estar atento quanto ao seguinte:  
  
-   Se o Agente de Distribuição ou o Agente de Mesclagem estiverem configurados para executar de modo contínuo, o agente aplica o instantâneo automaticamente, após a conclusão do Agente de Instantâneo.  
  
-   Se o Agente de Distribuição ou o Agente de Mesclagem estiverem configurados para executar em uma programação ou sob demanda, e não há instantâneos disponíveis quando o agente for executar, o agente será fechado exibindo uma mensagem indicando que o instantâneo não está disponível. Você deverá executar o agente novamente para aplicar o instantâneo após o Agente de Instantâneo ter concluído. Para mais informações sobre a execução de agentes, consulte [Sincronizar uma assinatura Push](../../../relational-databases/replication/synchronize-a-push-subscription.md), [Sincronizar uma assinatura Pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Conceitos dos executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
### <a name="should-i-script-my-replication-configuration"></a>Devo efetuar o script de minha configuração de replicação?  
 Sim. A realização do script da configuração da replicação é peça fundamental em qualquer plano de recuperação de desastres abrangendo uma topologia de replicação. Para obter mais informações sobre a realização de script, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
### <a name="what-recovery-model-is-required-on-a-replicated-database"></a>Que modelo de recuperação é requerido em um banco de dados replicado?  
 A replicação funciona corretamente seja qual for modelo de recuperação usado: simples, registrado em massa ou completo. A replicação de mesclagem rastreia a alteração armazenando as informações em tabelas de metadados. A replicação transacional rastreia as alterações marcando o log da transação, mas esse processo de marcação não é afetado pelo modelo de recuperação.  
  
### <a name="why-does-replication-add-a-column-to-replicated-tables-will-it-be-removed-if-the-table-isnt-published"></a>Por que a replicação adiciona uma coluna às tabelas replicadas, essa coluna será removida se a tabela não for publicada?  
 Para rastrear as alterações, a replicação de mesclagem e a replicação transacional, com assinaturas de atualização em fila, devem poder identificar exclusivamente cada linha em cada tabela publicada. Para realizar isso:  
  
-   A replicação de mesclarem adiciona a coluna **rowguid** a cada tabela, a menos que a tabela já tenha uma coluna de dados do tipo **uniqueidentifier** com a propriedade **ROWGUIDCOL** definida (neste caso esta coluna será usada). Se a tabela for descartada da publicação, a coluna **rowguid** será removida; mas, se uma coluna existente foi usada para o rastreamento, ela não será removida.  
  
-   Se uma publicação transacional tem suporte para assinaturas de atualização em fila, a replicação adicionará a coluna **msrepl_tran_version** a todas as tabelas. Se a tabela for descartada da publicação, a coluna **msrepl_tran_version** não será removida.  
  
-   Um filtro não deve incluir o **rowguidcol** usado por replicação para identificar linhas. Por padrão, esta é a coluna adicionada no momento que você define a replicação de mesclagem e é denominada **rowguid**.  
  
### <a name="how-do-i-manage-constraints-on-published-tables"></a>Como administrar as restrições em tabelas publicadas?  
 Há vários assuntos para serem considerados com relação à restrições em tabelas publicadas:  
  
-   A replicação transacional requer uma restrição de chave primária em cada tabela publicada. A replicação de mesclagem não requer nenhuma chave primária, mas se houver uma, ela deverá ser replicada. A replicação de instantâneos não requer nenhuma chave primária.  
  
-   Por padrão, as restrições de chave primária, os índices e as restrições de verificações são replicados nos Assinantes.  
  
-   A opção NOT FOR REPLICATION é especificada por padrão para as restrições de chave estrangeira e para as restrições de verificação; as restrições são impostas para operações de usuários mas não operações de agentes.  
  
 Para obter informações sobre como definir as opções de esquema que controlam se as restrições são replicadas, consulte [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
### <a name="how-do-i-manage-identity-columns"></a>Como gerenciar as colunas de identidade?  
 A replicação fornece um gerenciamento automático do intervalo de identidade para as topologias de replicação que incluem atualizações no Assinante. Para obter mais informações, consulte [Replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
### <a name="can-the-same-objects-be-published-in-different-publications"></a>Os mesmos objetos podem ser publicados em publicações diferentes?  
 Sim, mas com algumas restrições. Para mais informações, consulte a seção “Publicando tabelas em mais de uma publicação” no tópico [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
### <a name="can-multiple-publications-use-the-same-distribution-database"></a>Várias publicações podem usar o mesmo banco de dados de distribuição?  
 Sim. Não há nenhuma restrição sobre o número ou tipos de publicações que podem usar o mesmo banco de dados de distribuição. Todas as publicações de um determinado Publicador devem usar o mesmo Distribuidor e o mesmo banco de dados de distribuição.  
  
 Se há várias publicações, você pode configurar vários bancos de dados de distribuição no Distribuidor para certificar-se de que os dados fluindo em cada banco de dados de distribuição sejam de uma única publicação. Use a caixa de diálogo **Propriedades do distribuidor** ou o [sp_adddistributiondb &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) para adicionar um banco de dados de distribuição. Para mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="how-do-i-find-information-on-the-distributor-and-publisher-such-as-which-objects-in-a-database-are-published"></a>Como posso localizar as informações sobre o Distribuidor e o Publicador, tal como os objetos em um banco de dados que podem ser publicados?  
 Essas informações estão disponíveis por meio do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e dos vários procedimentos de replicação armazenados. Para obter mais informações, consulte [Distributor and Publisher Information Script](../../../relational-databases/replication/administration/distributor-and-publisher-information-script.md).  
  
### <a name="does-replication-encrypt-data"></a>A replicação criptografa dados?  
 Nenhum. A replicação não criptografa dados armazenados no banco de dados nem transferidos pela rede. Para obter mais informações, confira a seção "Criptografia" do tópico [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
### <a name="how-do-i-replicate-data-over-the-internet"></a>Como posso replicar dados pela Internet?  
 Replique os dados pela Internet, por meio de:  
  
-   Uma VPN (Virtual Private Network). Para obter mais informações, consulte [Publicar dados pela Internet usando VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md).  
  
-   Opção de sincronização da Web para replicação de mesclagem. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Todos os tipos de replicação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem replicar dados por uma VPN, no entanto, recomenda-se a sincronização da Web quando a replicação de mesclagem for utilizada.  
  
### <a name="does-replication-resume-if-a-connection-is-dropped"></a>A replicação será retomada se uma conexão for cancelada  
 Sim. O processamento de replicação é retomado no ponto em que ele foi interrompido quando a conexão foi cancelada. Se estiver usando uma replicação de mesclagem em uma rede não confiável, tente usar os registros lógicos, isto garantirá que as alterações sejam processadas como uma unidade. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
### <a name="does-replication-work-over-low-bandwidth-connections-does-it-use-compression"></a>A replicação trabalha em conexões de largura de banda baixa? Ela usa a compressão?  
 Sim, a replicação trabalha em conexões de largura de banda baixa Para conexões em TCP/IP, ela usa a compressão fornecida pelo protocolo, mas não fornece nenhuma compressão adicional. Em conexões de sincronização da Web em HTTPS, ela usa a compressão fornecida pelo protocolo e também a compressão adicional dos arquivos XML usados para replicar as alterações.  
  
## <a name="logins-and-object-ownership"></a>Propriedade de logons e de objetos  
  
### <a name="are-logins-and-passwords-replicated"></a>Os logons e as senhas são replicados?  
 Nenhum. Você pode criar um pacote SSIS para transferir os logons e as senhas do Publicador para um ou mais Assinantes.  
  
### <a name="what-are-schemas-and-how-are-they-replicated"></a>O que são os esquemas e como eles são replicados?  
 A começar pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *esquema* tem dois significados:  
  
-   A definição de um objeto, como uma instrução `CREATE TABLE`. Por padrão, a replicação copia as definições de todos os objetos replicados para o Assinante.  
  
-   O namespace no qual um objeto é criado: \<Banco de Dados>.\<Esquema>.\<Objeto>. Os esquemas são definidos usando a instrução `CREATE SCHEMA`.  
  
-   A replicação tem o seguinte comportamento padrão no Assistente para Nova Publicação em relação à propriedade de esquemas e objetos:  
  
-   Para artigos em publicações de mesclagem com um nível de compatibilidade 90 ou superior, publicações de instantâneos e publicações transacionais: por padrão, o proprietário do objeto no Assinante é igual ao proprietário do objeto correspondente no Publicador. Caso não existam esquemas proprietários de objetos no Assinante, eles serão criados automaticamente.  
  
-   Para artigos em publicação de mesclagem com um nível de compatibilidade abaixo de 90: por padrão, o proprietário é deixado em branco e especificado como **dbo** durante a criação do objeto no Assinante.  
  
-   Para artigos em publicações Oracle: por padrão, o proprietário é especificado como **dbo**.  
  
-   Para artigos em publicações que usam instantâneos de modo de caracteres (que são usados para Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Assinantes [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ): por padrão o proprietário é deixado em branco. O proprietário assume o padrão do proprietário associado à conta usada pelo Agente de Distribuição ou Agente de Mesclagem para se conectar ao Assinante.  
  
 O proprietário do objeto pode ser alterado por meio da caixa de diálogo **Propriedades do Artigo – \<***Artigo***>** e dos seguintes procedimentos armazenados: **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** e **sp_changemergearticle**. Para obter mais informações, consulte [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [Definir um artigo](../../../relational-databases/replication/publish/define-an-article.md) e [Exibir e modificar as propriedades do artigo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### <a name="how-can-grants-on-the-subscription-database-be-configured-to-match-grants-on-the-publication-database"></a>Como as concessões no banco de dados de assinatura podem ser configuradas para corresponder às concessões no banco de dados de publicação?  
 Por padrão, a replicação não executa instruções GRANT no banco de dados de assinatura. Se quiser que as permissões no banco de dados de assinatura correspondam àquelas no banco de dados de publicação, use um dos seguintes métodos:  
  
-   Execute as instruções GRANT diretamente no banco de dados de assinatura.  
  
-   Use um script de pós-instantâneo para executar as instruções. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](../../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  

 
-   Use o procedimento armazenado [sp_addscriptexec](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) para executar as instruções.  
  
### <a name="what-happens-to-permissions-granted-in-a-subscription-database-if-a-subscription-is-reinitialized"></a>O que acontece às permissões concedidas em um banco de dados de assinatura se uma assinatura for reinicializada?  
 Por padrão, os objetos no Assinante são cancelados e criados novamente quando uma assinatura é reinicializada, isto que faz com que todas as permissões concedidas para aqueles objetos sejam canceladas. Há dois modos para controlar isto:  
  
-   Aplique novamente as concessões após a reinicialização, usando as técnicas descritas na seção anterior.  
  
-   Especifique que os objetos não devem ser descartados quando a assinatura for reinicializada. Antes da reinicialização, você deve:  
  
    -   Execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) ou [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor igual a 'pre_creation_cmd' (**sp_changearticle**) ou 'pre_creation_command' (**sp_changemergearticle**) para o parâmetro `@property` e um valor igual a 'none', 'delete' ou 'truncate' para o parâmetro `@value`.  
  
    -   Na caixa de diálogo **Propriedades do Artigo – \<Artigo>** na seção **Objeto de Destino**, selecione um valor **Manter objeto existente inalterado**, **Excluir dados. Se o artigo tiver um filtro de linha, exclua somente os dados correspondentes ao filtro.** ou **Truncar todos os dados no objeto existente** para a opção **Ação se o nome estiver em uso**. Para mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## <a name="database-maintenance"></a>Manutenção do banco de dados  
  
### <a name="why-cant-i-run-truncate-table-on-a-published-table"></a>Por que não consigo executar TRUNCATE TABLE em uma tabela publicada?  
 TRUNCATE TABLE é uma instrução DDL que não registra exclusões de linha individuais e não aciona os gatilhos DML. Isso não é permitido, pois a replicação não pode rastrear as alterações causadas pela operação: a replicação transacional rastreia as alterações por meio do log de transações; a replicação de mesclagem rastreia as alterações por meio de gatilhos DML nas tabelas publicadas.  
  
### <a name="what-is-the-effect-of-running-a-bulk-insert-command-on-a-replicated-database"></a>Qual é o efeito de se executar um comando de inserção em massa em um banco de dados replicado?  
 Para a replicação transacional, as inserções em massa são rastreadas e replicadas como as demais inserções. Para a replicação de mesclagem, você deve certificar-se de que os metadados de rastreamento de alterações estejam corretamente atualizados.  
  
### <a name="are-there-any-replication-considerations-for-backup-and-restore"></a>Existem algumas considerações para o backup e a restauração?  
 Sim. Existem várias considerações especiais para os bancos de dados envolvidos em replicação. Para obter mais informações, veja [Fazer backup e restaurar bancos de dados replicados](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
### <a name="does-replication-affect-the-size-of-the-transaction-log"></a>A replicação afeta o tamanho do log de transações?  
 A replicação de mesclagem e a replicação de instantâneos não afetam o tamanho do log de transações, mas uma replicação transacional sim. Se um banco de dados incluir uma ou mais publicações transacionais, o log não será truncado até que todas as transações pertinentes para as publicações sejam enviadas ao banco de dados de distribuição. Se o log de transações aumentar demasiadamente, e o Agente de Leitor de Log estiver em execução com agendamento definido, considere encurtar o intervalo entre as execuções. Ou, defina-o para executar em modo contínuo. Se ele for definido para executar em modo contínuo (o padrão), garanta que ele esteja em execução. Para obter mais informações sobre como verificar o status do agente de leitor de Log, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Além disso, se você tiver definido a opção 'sync with backup' no banco de dados de publicação ou no banco de dados de distribuição, o log de transações não será truncado até o backup de todas as transações ser feito. Se o log de transações crescer demasiadamente, e você tiver essa opção definida, considere encurtar o intervalo entre os backups do log de transações. Para mais informações sobre backup e restauração de bancos de dados envolvidos na replicação transacional, consulte [Estratégias de backup e restauração de instantâneo e replicação transacional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="how-do-i-rebuild-indexes-or-tables-in-replicated-databases"></a>Como posso reconstruir índices ou tabelas em bancos de dados replicados?  
 Há vários mecanismos para reconstruir índices. Todos podem ser usados sem considerações especiais para a replicação, exceto pelo seguinte: as chaves primárias são necessárias para as tabelas em publicações transacionais, portanto você não pode cancelar e recriar chaves primárias nessas tabelas.  
  
### <a name="how-do-i-add-or-change-indexes-on-publication-and-subscription-databases"></a>Como posso adicionar ou alterar índices em bancos de dados de publicação e de assinatura?  
 Índices podem ser adicionados no Publicador ou nos Assinantes sem considerações especiais para a replicação (lembre-se de que os índices podem afetar o desempenho). `CREATE INDEX` e `ALTER INDEX` não são replicados, portanto, ao adicionar ou alterar um índice no Publicador, por exemplo, deve-se fazer a mesma adição ou alteração no Assinante para que ele esteja refletido lá.  
  
### <a name="how-do-i-move-or-rename-files-for-databases-involved-in-replication"></a>Como posso mover ou renomear arquivos para bancos de dados envolvidos em replicação?  
 Em versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], para mover ou renomear arquivos de banco de dados era necessário desanexar e tornar a anexar o banco de dados. Como um banco de dados replicado não pode ser desanexado, a replicação devia ser removida antes que os bancos de dados. A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], é possível mover ou renomear arquivos sem desanexar e anexar novamente o banco de dados, e não produzir efeito sobre a replicação. Para mais informações sobre as operações de renomeação e movimentação, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md).  
  
### <a name="how-do-i-drop-a-table-that-is-being-replicated"></a>Como posso descartar uma tabela que está sendo replicada?  
 Primeiro, remova o artigo da publicação usando [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) ou a caixa de diálogo **Propriedades de Publicação – \<Publicação>**, em seguida, remova-o do banco de dados usando `DROP <Object>`. Não é possível descartar artigos de publicações transacionais ou de instantâneos após as assinaturas terem sido adicionadas; antes é preciso descartar as assinaturas. Para obter mais informações, consulte [Add Articles to and Drop Articles from Existing Publications](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
### <a name="how-do-i-add-or-drop-columns-on-a-published-table"></a>Como posso adicionar ou descartar colunas em uma tabela publicada?  
 O[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a uma grande variedade de alterações de esquema em objetos publicados, inclusive a adição e o descarte de colunas. Por exemplo, execute `ALTER TABLE … DROP COLUMN` no Publicador e a instrução será replicada para os Assinantes, em seguida, será executada para descartar a coluna. Os Assinantes executando versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] possuem suporte para a adição e descarte de colunas por meio dos procedimentos armazenados [sp_repladdcolumn](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) e [sp_repldropcolumn](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md). Para obter mais informações, consulte [Make Schema Changes on Publication Databases](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md) (Fazer alterações de esquema em bancos de dados de publicação).  
  
## <a name="replication-maintenance"></a>Manutenção da Replicação  
  
### <a name="how-do-i-determine-if-the-data-at-subscribers-is-synchronized-with-data-at-the-publisher"></a>Como posso determinar se os dados no Assinante estão sincronizados com os dados no Publicador?  
 Use a validação. A validação informa se um determinado Assinante está sincronizado com o Publicador. Para obter mais informações, consulte [Validar os dados replicados](../../../relational-databases/replication/validate-data-at-the-subscriber.md). A validação não fornece qualquer informação sobre possíveis linhas sincronizadas incorretamente, mas a [utilidade tablediff](../../../tools/tablediff-utility.md) faz isso.  
  
### <a name="how-do-i-add-a-table-to-an-existing-publication"></a>Como posso adicionar uma tabela a uma publicação existente?  
 Não é necessário interromper a atividade no banco de dados de publicação ou de assinatura para adicionar uma tabela (ou qualquer outro objeto). Adicione uma tabela a uma publicação com a caixa de diálogo **Propriedades de Publicação – \<Publicação>** ou os procedimentos armazenados [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Para obter mais informações, consulte [Add Articles to and Drop Articles from Existing Publications](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
### <a name="how-do-i-remove-a-table-from-a-publication"></a>Como posso remover uma tabela de uma publicação?  
 Remova a tabela da publicação usando [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), [sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) ou a caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Não é possível descartar artigos de publicações transacionais ou de instantâneos após as assinaturas terem sido adicionadas; antes é preciso descartar as assinaturas. Para obter mais informações, consulte [Add Articles to and Drop Articles from Existing Publications](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
### <a name="what-actions-require-subscriptions-to-be-reinitialized"></a>Que ações exigem que as assinaturas sejam reinicializadas?  
 Há várias alterações em artigos e publicações que exigem a reinicialização das assinaturas. Para obter mais informações, consulte [Alterar propriedade da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### <a name="what-actions-cause-snapshots-to-be-invalidated"></a>Que ações fazem com que os instantâneos sejam invalidados?  
 Há várias alterações em artigos e publicações que invalidam os instantâneos e exigem a geração de um novo instantâneo. Para obter mais informações, consulte [Alterar propriedade da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### <a name="how-do-i-remove-replication"></a>Como posso remover a replicação?  
 As ações necessárias à remoção de replicação de banco de dados dependem se o banco de dados foi usado como um banco de dados de publicação, banco de dados de assinatura ou ambos.  
  
### <a name="how-do-i-determine-whether-there-are-transactions-or-rows-to-be-replicated"></a>Como posso determinar se há transações ou linhas a serem replicadas?  
 Para a replicação transacional, use os procedimentos armazenados ou a guia **Comandos não Distribuídos** no Replication Monitor. Para obter mais informações, confira [Exibir comandos replicados e outras informações no banco de dados de distribuição &#40;Programação do Transact-SQL de replicação&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md) e [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Para replicação de mesclagem, use o procedimento armazenado **sp_showpendingchanges**. Para mais informações, consulte [sp_showpendingchanges &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md).  
  
### <a name="how-far-behind-is-the-distribution-agent-should-i-reinitialize"></a>O Agente de Distribuição está muito lento? Devo reinicializar?  
 Use o procedimento armazenado **sp_replmonitorsubscriptionpendingcmds** ou a guia **Comandos não Distribuídos** no Replication Monitor. O procedimento armazenado e a guia exibem:  
  
-   O número de comandos no banco de dados de distribuição que não foram entregues ao Assinante selecionado. Um comando consiste em uma instrução DML (linguagem de manipulação de dados) ou uma instrução DDL (linguagem de definição de dados) Transact-SQL.  
  
-   A quantidade de tempo estimada para entrega de comandos ao Assinante. Se esse valor for maior do que a quantidade de tempo requerida para gerar e aplicar um instantâneo ao Assinante, considere reiniciar o Assinante. Para obter mais informações, consulte [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
 Para obter mais informações, confira [sp_replmonitorsubscriptionpendingcmds &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md) e [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="replication-and-other-database-features"></a>Replicação e demais recursos dos Bancos de Dados  
  
### <a name="does-replication-work-in-conjunction-with-log-shipping-and-database-mirroring"></a>A replicação trabalha junto com o envio de logs e espelhamento de banco de dados?  
 Sim. Para mais informações, consulte [Replicação e envio de logs &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) e [Espelhamento de banco de dados e replicação &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
### <a name="does-replication-work-in-conjunction-with-clustering"></a>A replicação trabalha junto com o uso de cluster?  
 Sim. Nenhuma consideração especial é exigida porque todos os dados são armazenados em um conjunto de discos no cluster.  
  
## <a name="see-also"></a>Consulte Também  
 [Perguntas Frequentes sobre Administração de Replicação](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
