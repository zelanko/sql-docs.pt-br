---
title: Fazer alterações de esquema em bancos de dados de publicação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- snapshot replication [SQL Server], replicating schema changes
- merge replication [SQL Server replication], replicating schema changes
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
- publishing [SQL Server replication], schema changes
ms.assetid: 926c88d7-a844-402f-bcb9-db49e5013b69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65436da64ca7c718de053dab520edad71dac6228
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68199456"
---
# <a name="make-schema-changes-on-publication-databases"></a>Fazer alterações de esquema em bancos de dados de publicação
  A replicação oferece suporte para um amplo intervalo de alterações de esquema para objetos publicados. Ao se fazer qualquer uma das seguintes alterações de esquema no objeto publicado adequado em um Editor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], essa alteração será propagada por padrão para todos os Assinantes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   ALTER TABLE  
  
-   ALTER TABLE SET LOCK ESCALATION não deverá ser usado se a replicação da alteração de esquema estiver habilitada e uma topologia incluir [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssEWnoversion](../../../includes/ssewnoversion-md.md)] Subscribers.ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
     ALTER TRIGGER pode ser usado somente para gatilhos DML [linguagem de manipulação de dados], pois os gatilhos DDL [linguagem de definição de dados] não podem ser replicados.  
  
> [!IMPORTANT]  
>  As alterações de esquema para tabelas devem ser feitas usando-se [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou SMO ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects). Quando alterações de esquema forem feitas em [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] tenta descartar e recriar a tabela. Não é possível descartar objetos publicados; portanto, há falha na alteração de esquema.  
  
 Para replicação transacional e replicação de mesclagem, alterações de esquema são propagadas de forma incremental quando o Distribution Agent ou o Merge Agent são executados. Para replicação de instantâneo, alterações de esquema são propagadas quando um instantâneo novo for aplicado ao Assinante. Em replicação de instantâneo, uma cópia nova do esquema é enviada ao Assinante a cada vez que ocorrer sincronização. Assim, todas as alterações de esquema (não apenas aquelas listadas acima) para objetos previamente publicados são propagadas automaticamente com cada sincronização.  
  
 Para obter informações sobre como adicionar e remover artigos de publicações, consulte [Adicionar e remover artigos de publicações existentes](add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **Para replicar alterações de esquema**  
  
 As alterações de esquema listadas acima são replicadas por padrão. Para obter informações sobre como desabilitar a replicação de alterações de esquema, consulte [Replicate Schema Changes](replicate-schema-changes.md).  
  
## <a name="considerations-for-schema-changes"></a>Considerações para alterações de esquema  
 Lembre-se das seguintes considerações ao replicar alterações de esquema.  
  
### <a name="general-considerations"></a>Considerações gerais  
  
-   As alterações de esquema estão sujeitas a qualquer restrição imposta por [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Por exemplo, ALTER TABLE não lhe permite ALTER colunas de chave primária.  
  
-   O mapeamento de tipo de dados só é executado para o instantâneo inicial. As alterações de esquema não são mapeadas para versões anteriores de tipos de dados. Por exemplo, se a instrução `ALTER TABLE ADD datetime2 column` for usada no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], o tipo de dados não será convertido em `nvarchar` para Assinantes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Em alguns casos, as alterações de esquema são bloqueadas no Publicador.  
  
-   Se uma publicação é definida para permitir a propagação de alterações de esquema, alterações de esquema são propagadas independentemente de como a opção de esquema correspondente é definida para um artigo na publicação. Por exemplo, se você selecionar não replicar restrições de chave estrangeira para um artigo de tabela, mas então emitir um comando ALTER TABLE que adiciona uma chave estrangeira à tabela no Publicador, a chave estrangeira será acrescentada à tabela no Assinante. Para evitar isso, desabilite a propagação de alterações de esquema antes de emitir o comando ALTER TABLE.  
  
-   As alterações de esquema devem ser feitas somente no Publicador, não em Assinantes (inclusive Assinantes de republicação). Replicação de mesclagem evita alterações de esquema no Assinante. Replicação transacional não evita as alterações, mas as alterações podem levar à falha da replicação.  
  
-   Alterações propagadas para um Assinante de republicação são, por padrão, propagadas para seus Assinantes.  
  
-   Se a alteração de esquema faz referência a objetos ou restrições existentes no Publicador mas não no Assinante, a alteração de esquema tem êxito no Publicador mas não no Assinante.  
  
-   Todos os objetos no Assinante que são referenciados ao se adicionar uma chave estrangeira devem ter o mesmo nome e proprietário que o objeto correspondente no Publicador.  
  
-   Não há suporte ao se adicionar, descartar ou alterar índices explicitamente. Índices criados implicitamente para restrições (como uma restrição de chave primária) têm suporte.  
  
-   Não há suporte ao se alterar ou descartar colunas de identidade gerenciadas por replicação. Para obter mais informações sobre o gerenciamento automático de colunas de identidade, consulte [Replicar colunas de identidade](replicate-identity-columns.md).  
  
-   As alterações de esquema que incluem funções não determinísticas não têm suporte, pois podem resultar em dados diferentes no Publicador e no Assinante (o que é chamado de não convergência). Por exemplo, se você emitir o seguinte comando no Publicador: `ALTER TABLE SalesOrderDetail ADD OrderDate DATETIME DEFAULT GETDATE()`, os valores são diferentes quando o comando é replicado para o Assinante e executado. Para obter mais informações sobre funções não determinísticas, consulte [Deterministic and Nondeterministic Functions](../../user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
-   Recomenda-se que restrições sejam nomeadas explicitamente. Se uma restrição não for nomeada explicitamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerará um nome para a restrição e esses nomes serão diferentes no Publicador e em cada Assinante. Isso pode causar problemas durante a replicação de alterações de esquema. Por exemplo, se você descartar uma coluna no Publicador e uma restrição dependente for descartada, a replicação tentará descartar a restrição no Assinante. O descarte no Assinante irá falhar porque o nome da restrição é diferente. Se a sincronização falhar devido a um problema de nomeação de restrição, descarte manualmente a restrição no Assinante e, então, execute novamente o Merge Agent.  
  
-   Se uma tabela é publicada para replicação, não é possível alterar uma coluna naquela tabela para um tipo de dados XML se um instantâneo de publicação já tiver sido gerado. Para alterar a coluna, você deve primeiramente remover a replicação.  
  
-   Leitura não confirmada não é um nível de isolamento com suporte ao fazer o DDL em uma tabela publicada.  
  
-   `SET CONTEXT_INFO` não deve ser usado para modificar o contexto de transações em que as alterações de esquema são executadas em objetos publicados.  
  
#### <a name="adding-columns"></a>Adicionando colunas  
  
-   Para adicionar uma nova coluna a uma tabela e incluir essa coluna em uma publicação existente, execute ALTER TABLE \<Table> ADD \<Column>. Por padrão, a coluna é replicada para todos os Assinantes. A coluna deve permitir valores NULL ou incluir uma restrição padrão. Para obter mais informações sobre como adicionar colunas, consulte a seção “Replicação de mesclagem” neste tópico.  
  
-   Para adicionar uma nova coluna a uma tabela sem incluir essa coluna em uma publicação existente, desabilite a replicação de alterações de esquema e, em seguida, execute ALTER TABLE \<Table> ADD \<Column>.  
  
-   Para incluir uma coluna existente em uma publicação existente, use [sp_articlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql), [sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) ou a caixa de diálogo **Propriedades da Publicação – \<Publicação>**.  
  
     Para obter mais informações, consulte [Definir e modificar um filtro de colunas](define-and-modify-a-column-filter.md). Isso exigirá que as assinaturas sejam reinicializadas.  
  
-   Não há suporte para adicionar uma coluna de identidade a uma tabela publicada, pois isso pode resultar em não convergência quando a coluna é replicada no Assinante. Os valores na coluna de identidade no Publicador dependerão da ordem em que as linhas para a tabela afetada forem armazenadas fisicamente. As linhas podem ser armazenadas de forma diversa no Assinante; assim, o valor da coluna de identidade pode ser diferente para as mesmas linhas.  
  
#### <a name="dropping-columns"></a>Descartando colunas  
  
-   Para remover uma coluna de uma publicação existente e remover a coluna da tabela no Publicador, execute ALTER TABLE \<Table> DROP \<Column>. Por padrão, a coluna é então descartada da tabela em todos os Assinantes.  
  
-   Para remover uma coluna de uma publicação existente, mas manter a coluna na tabela no Publicador, use [sp_articlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql), [sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) ou a caixa de diálogo **Propriedades da Publicação – \<Publicação>**.  
  
     Para obter mais informações, consulte [Definir e modificar um filtro de colunas](define-and-modify-a-column-filter.md). Isso exigirá a geração de um instantâneo novo.  
  
-   A coluna a ser descartada não pode ser usada nas cláusulas de filtro de nenhum artigo de nenhuma publicação no banco de dados.  
  
-   Ao descartar uma coluna de um artigo publicado, considere quaisquer restrições, índices ou propriedades da coluna que possam afetar o banco de dados. Por exemplo:  
  
    -   Não é possível descartar colunas usadas em uma chave primária de artigos em publicações transacionais, uma vez que elas são usadas pela replicação.  
  
    -   Não é possível descartar a coluna rowguid de artigos em publicações de mesclagem ou a coluna mstran_repl_version de artigos em publicações transacionais que suportam assinaturas de atualização, uma vez que elas são usadas pela replicação.  
  
    -   As alterações de índices não são propagadas para Assinantes: se você descartar uma coluna no Publicador e um índice dependente for descartado, o índice descartado não será replicado. Deve-se descartar o índice no Assinante antes de descartar as colunas no Publicador, de forma que o descarte da coluna tenha êxito quando for replicado do Publicador para o Assinante. Se a sincronização falhar devido a um índice no Assinante, descarte manualmente o índice e, então, execute novamente o Merge Agent.  
  
    -   Restrições devem ser explicitamente nomeadas para permitir que sejam descartadas. Para obter mais informações, consulte a seção "Considerações gerais" anteriormente neste tópico.  
  
### <a name="transactional-replication"></a>Replicação transacional  
  
-   As alterações de esquema são propagadas para Assinantes que estão executando versões anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mas a instrução DDL deverá incluir apenas sintaxe que tenha suporte da versão do Assinante.  
  
     Se o Assinante republicar dados, as únicas alterações de esquema com suporte incluem adicionar e descartar uma coluna. Essas alterações devem ser feitas no Publicador usando [sp_repladdcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) e [sp_repldropcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql) em vez da sintaxe ALTER TABLE DDL.  
  
-   Não são replicadas alterações de esquema a Assinantes de não SQL Server.  
  
-   As alterações de esquema não são propagadas de Publicadores não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Não é possível alterar exibições indexadas que são replicadas como tabelas. Exibições indexadas que são replicadas como exibições indexadas podem ser alteradas, mas sua alteração irá fazer com que sejam exibições regulares e não exibições indexadas.  
  
-   Se a publicação oferecer suporte à atualização imediata ou a assinaturas de atualização enfileirada, o sistema deverá ser confirmado antes que sejam feitas alterações de esquema: toda atividade na tabela publicada deve ser interrompida no Publicador e nos Assinantes, e as alterações de dados pendentes deverão ser propagadas para todos os nós. Depois que as alterações de esquema tenham se propagado para todos os nós, a atividade pode ser retomada nas tabelas publicadas.  
  
-   Se a publicação estiver em uma topologia ponto a ponto, o sistema deve ser confirmado antes que sejam feitas alterações de esquema. Para obter mais informações, consulte [Como confirmar uma topologia de replicação &#40;Programação Transact-SQL de replicação&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   O adição de uma coluna de carimbo e o mapeamento do carimbo para binário(8) levam o artigo a ser reinicializado para todas as assinaturas ativas.  
  
### <a name="merge-replication"></a>Replicação de mesclagem  
  
-   A maneira como a replicação de mesclagem trata alterações de esquema é determinada pelo nível de compatibilidade da publicação e pela definição do instantâneo como modo nativo (padrão) ou modo de caractere:  
  
    -   Para replicar alterações de esquema, o nível de compatibilidade da publicação deve ser pelo menos 90RTM. Se os Assinantes estiverem executando versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o nível de compatibilidade for inferior a 90RTM, você poderá usar [sp_repladdcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) e [sp_repldropcolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql) para adicionar e remover colunas. Porém, estes procedimentos não são recomendados.  
  
    -   Se você tentar adicionar a um artigo existente uma coluna com um tipo de dados que foi lançado no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] terá o seguinte comportamento:  
  
        ||100RTM, instantâneo nativo|100RTM, instantâneo de caractere|Todos os outros níveis de compatibilidade|  
        |-|-----------------------------|--------------------------------|------------------------------------|  
        |`hierarchyid`|Permitir alteração|Bloquear alteração|Bloquear alteração|  
        |`geography` e `geometry`|Permitir alteração|Permitir alteração<sup>1</sup>|Bloquear alteração|  
        |`filestream`|Permitir alteração|Bloquear alteração|Bloquear alteração|  
        |`date`, `time`, `datetime2` e `datetimeoffset`|Permitir alteração|Permitir alteração<sup>1</sup>|Bloquear alteração|  
  
         <sup>1</sup> os assinantes do SQL Server Compact convertem esses tipos de dados no Assinante.  
  
-   Se um erro ocorrer ao ser aplicada uma alteração de esquema (como um erro resultante da adição de uma chave estrangeira que faz referência a uma tabela não disponível no Assinante), a sincronização falhará e a assinatura deverá ser reinicializada.  
  
-   Se uma alteração de esquema for feita em uma coluna envolvida em um filtro de junção ou filtro com parâmetros, deve reinicializar-se todas as assinaturas e gerar novamente o instantâneo.  
  
-   A replicação de mesclagem leva os procedimentos armazenados a ignorar alterações de esquema durante a solução de problemas. Para obter mais informações, consulte [sp_markpendingschemachange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql) e [sp_enumeratependingschemachanges &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER VIEW &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-view-transact-sql)   
 [ALTER PROCEDURE &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-procedure-transact-sql)   
 [ALTER FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-function-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [Publicar objetos de banco de dados e](publish-data-and-database-objects.md)   
 [Regenerar os procedimentos transacionais personalizados para refletir alterações de esquema](../transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)  
  
  
