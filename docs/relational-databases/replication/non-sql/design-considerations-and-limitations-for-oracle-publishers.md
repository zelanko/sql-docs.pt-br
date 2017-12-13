---
title: "Considerações de design e limitações para Publicadores Oracle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Oracle publishing [SQL Server replication], design considerations and limitations
ms.assetid: 8d9dcc59-3de8-4d36-a61f-bc3ca96516b6
caps.latest.revision: "48"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 960d338d40732d53e5734ec9666e7d926a2b7a22
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="design-considerations-and-limitations-for-oracle-publishers"></a>Considerações de design e limitações para Publicadores Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A publicação de um banco de dados Oracle é projetada para funcionar de forma praticamente idêntica à publicação de um banco de dados [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Porém, deve-se estar atento às seguintes limitações e problemas:  
  
-   A opção Oracle Gateway fornece desempenho melhorado em relação à opção Oracle Complete; entretanto, essa opção não pode ser usada para publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo. Se você precisa publicar a mesma tabela em várias publicações transacionais, escolha a opção Oracle Complete.  
  
-   Replicação oferece suporte para tabelas de publicação, índices e exibições materializadas. Outros objetos não são replicados.  
  
-   Há algumas pequenas diferenças entre o armazenamento e o processamento de dados no Oracle e em bancos de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que afetam a replicação.  
  
-   Há várias diferenças relativas à maneira como recursos de replicação transacionais oferecem suporte ao usar um Editor Oracle.  
  
## <a name="support-for-publishing-objects-from-oracle"></a>Suporte para publicar objetos do Oracle  
 A replicação oferece suporte para replicar os seguintes objetos de bancos de dados do Oracle:  
  
-   Tabelas  
  
-   Tabelas organizadas por índice  
  
-   Índices  
  
-   Exibições materializadas (replicadas como tabelas)  
  
 Os seguintes itens podem estar presentes em tabelas publicadas mas não são replicados:  
  
-   Índices com base em domínio  
  
-   Índices com base em função  
  
-   Padrões  
  
-   Verificar restrições  
  
-   Chaves estrangeiras  
  
-   Opções de armazenamento (tablespaces, clusters etc.)  
  
 Os seguintes objetos não podem ser replicados:  
  
-   Tabelas aninhadas  
  
-   Exibições  
  
-   Pacotes, corpos de pacote, procedimentos e gatilhos  
  
-   Filas  
  
-   Sequências  
  
-   Sinônimos  
  
 Para obter mais informações sobre tipos de dados com suporte, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
## <a name="differences-between-oracle-and-sql-server"></a>Diferenças entre Oracle e SQL Server  
  
-   Oracle tem limites de tamanho máximo diferentes para alguns objetos. Quaisquer objetos criados no banco de dados de publicação Oracle devem aderir aos limites máximos de tamanho para os objetos correspondentes em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para mais informações sobre limites em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Especificações de capacidade máxima do SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
-   Por padrão nomes de objeto do Oracle são criados com maiúscula. Certifique-se de fornecer os nomes de objetos Oracle em maiúscula ao publicá-los por meio de um Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se eles tiverem maiúscula no banco de dados do Oracle. Falha ao especificar os objetos com maiúscula ou minúscula pode resultar em uma mensagem de erro indicando que o objeto não pode ser encontrado.  
  
-   O Oracle tem um dialeto de SQL ligeiramente diferente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; filtros de linha devem ser gravados em sintaxe compatível com Oracle.  
  
### <a name="considerations-for-large-objects"></a>Considerações para objetos grandes  
 Dados de objeto grande (LOB) não são armazenados na tabela de log de artigo; atualizações para dados LOB são sempre recuperados diretamente da tabela publicada. Atualizações são replicadas em publicações transacionais somente se a operação que afete LOB acionar gatilhos de replicação na tabela replicada. Gatilhos Oracle são acionados quando linhas contendo LOBs são inseridas ou excluídas; entretanto, atualizações para colunas LOB não disparam gatilhos. Uma atualização para uma coluna LOB será replicada imediatamente somente se a coluna não LOB da mesma linha também for atualizada na mesma transação Oracle. Caso contrário, a coluna LOB será atualizada no Assinante quando a próxima atualização para uma coluna não LOB ocorrer na mesma linha. Verifique se esse comportamento é aceitável para seu aplicativo.  
  
 Para replicar atualizações para colunas LOB em publicações transacionais, considere uma das seguintes estratégias ao gravar o aplicativo:  
  
-   Exclua e volte a inserir as linhas em uma transação em vez de atualizar a linha: especifique a nova LOB ao reinserir a linha. Por excluir e inserir os dois gatilhos, a linha será replicada.  
  
-   Inclua uma coluna não LOB na atualização de linha além da coluna LOB ou atualize uma coluna não LOB da linha como parte da mesma transação Oracle. Em ambos os casos, a atualização da coluna não LOB assegura o acionamento do gatilho.  
  
 Para obter mais informações sobre LOBs, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
### <a name="unique-indexes-and-constraints"></a>Índices e restrições exclusivos  
 Tanto para replicação de instantâneo quanto para a replicação transacional, as colunas contidas em índices e restrições exclusivos (incluindo restrições de chave primária) devem se ater a determinadas restrições. Se não aderirem a essas restrições, a restrição ou índice não é replicado.  
  
-   O número máximo de colunas permitido em um índice em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é 16.  
  
-   Todas as colunas incluídas em restrições exclusivas devem ter tipos de dados com suporte. Para obter mais informações sobre tipos de dados, consulte [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
-   Todas as colunas incluídas em restrições exclusivas devem ser publicadas (não podem ser filtradas).  
  
-   Colunas envolvidas em restrições ou índices exclusivos não devem ser nulas.  
  
 Considere também os seguintes problemas:  
  
-   A Oracle e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tratam o NULL diferentemente: a Oracle permite várias linhas com valores nulos para colunas que permitem o NULL e são incluídas em restrições ou índices exclusivos. O[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] impõe exclusividade permitindo somente uma única linha com um valor nulo para a mesma coluna. Não é possível publicar uma restrição ou índice exclusivo que permita NULL uma vez que haveria uma violação de restrição no Assinante se a tabela publicada tiver várias linhas com valores NULL para qualquer uma das colunas incluídas no índice ou restrição.  
  
-   Ao testar exclusividade, espaços em branco em um campo são ignorados por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mas não pelo Oracle.  
  
 Assim como na replicação transacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , as tabelas em publicações transacionais do Oracle exigem uma chave primária; a chave primária deve ser exclusiva com base nas regras acima especificadas. Se a chave primária não aderir às regras definidas nos pontos anteriores, a tabela não pode ser publicada para replicação transacional.  
  
## <a name="differences-between-oracle-publishing-and-standard-transactional-replication"></a>Diferenças entre publicação do Oracle e replicação transacional padrão  
  
-   Um Editor Oracle não pode ter o mesmo nome de seu Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o mesmo nome que qualquer um dos Editores [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usam o Distribuidor ou que qualquer Assinante que recebe a publicação. Publicações com o mesmo Distribuidor devem ter cada uma um nome exclusivo.  
  
-   Uma tabela publicada em uma publicação do Oracle não pode receber dados replicados. Assim, a publicação do Oracle não oferece suporte para: publicações com assinaturas de atualização imediata ou enfileirada; ou topologias nas quais tabelas de publicação também funcionam com tabelas de assinatura, tais como replicação ponto a ponto e bidirecional.  
  
-   Chave primária para relações da chave estrangeira no banco de dados Oracle não é replicada para Assinantes. Porém, os relações são mantidas nos dados conforme as alterações são aplicadas.  
  
-   Publicações transacionais padrão oferecem suporte para tabelas de até 1000 colunas. Publicações transacionais Oracle oferecem suporte para 995 colunas (a replicação adiciona cinco colunas a cada tabela publicada).  
  
-   Cláusulas de agrupamento são adicionadas às instruções CREATE TABLE para habilitar comparações que diferenciam maiúscula de minúscula, o que é importante para chaves primárias e restrições exclusivas. Este comportamento é controlado com a opção de esquema 0x1000, especificada com o parâmetro **@schema_option** de [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Se você usar procedimentos armazenados para configurar ou manter um Editor Oracle, não coloque os procedimentos dentro de uma transação explícita. Isso não oferece suporte sobre o servidor vinculado usado para conexão com o Editor Oracle.  
  
-   Se você criar uma assinatura pull para uma publicação do Oracle com um assistente, deve-se usar o Assistente para Nova Assinatura fornecido com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores. Para versões anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é possível, entretanto, usar o procedimento armazenado e interfaces SQL-DMO para configurar assinaturas pull para publicações do Oracle.  
  
-   Se usar procedimentos armazenados para propagar alterações para Assinantes (o padrão), lembre-se de que a sintaxe MCALL tem suporte, mas tem um comportamento diferente quando a publicação é de um Editor Oracle. Normalmente, MCALL fornece um bitmap que mostra que colunas foram atualizadas no Publicador. Com uma publicação do Oracle, o bitmap sempre mostra que todas as colunas foram atualizadas. Para mais informações sobre o uso de procedimentos armazenados, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
### <a name="transactional-replication-feature-support"></a>Suporte de recursos de replicação transacional  
  
-   As publicações do Oracle não oferecem suporte para todas as opções de esquema que as publicações do SQL Server oferecem suporte. Para obter mais informações sobre opções de esquema, consulte [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Assinantes de publicações do Oracle não podem usar assinaturas de atualização imediata ou enfileiradas ou ser nós em uma topologia ponto a ponto ou bidirecional.  
  
-   Assinantes de publicações do Oracle não podem ser inicializados automaticamente de um backup.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte para dois tipos de validação: binária e de contagem de linhas. Publicadores Oracle oferecem suporte para validação de contagem de linhas. Para obter mais informações, consulte [Validar os dados replicados](../../../relational-databases/replication/validate-replicated-data.md).  
  
-   O[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece dois formatos de instantâneo: modo de bcp nativo e modo de caractere. Publicadores Oracle oferecem suporte para instantâneos de modo de caractere.  
  
-   Alterações de esquema para tabelas do Oracle publicadas não têm suporte. Para executar alterações de esquema, primeiro descarte a publicação, faça as alterações e, então, crie novamente a publicação e quaisquer assinaturas.  
  
    > [!NOTE]  
    >  Se as alterações de esquema e subsequente cancelamento e recriação da publicação e assinaturas forem executados em um momento em que nenhuma atividade estiver ocorrendo nas tabelas publicadas, pode-se especificar a opção ‘suporte para replicação somente' para as assinaturas. Isso lhes permite ser sincronizados sem ter de copiar um instantâneo para cada Assinante. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="replication-security-model"></a>Modelo de segurança de replicação  
 O modelo de segurança para publicação do Oracle é o mesmo que o modelo de segurança para replicação transacional padrão, com as seguintes exceções:  
  
-   A conta sob a qual o Snapshot Agent e o Log Reader Agent fazem conexões do Distribuidor para o Processador é especificada por um dos seguintes métodos:  
  
    -   O parâmetro **@security_mode** do [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) (você também especifica valores para **@login** e **@password** se for usada a autenticação do Oracle)  
  
    -   Na caixa de diálogo **Conectar ao Servidor** no SQL Server Management Studio, que você usa ao configurar o Editor Oracle no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Na replicação transacional padrão, a conta é especificada com [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) e [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md).  
  
-   A conta sob a qual o Snapshot Agent e o Agente de Leitor de Log fazem conexões não pode ser alterada com [sp_changedistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) ou por uma folha de propriedades, mas a senha pode ser alterada.  
  
-   Se você especificar um valor de 1 (Autenticação Integrada do Windows) para o parâmetro **@security_mode** de [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md):  
  
    -   A conta e a senha de processo usadas para o Snapshot Agent e o Agente de Leitor de Log (os parâmetros **@job_login** e **@job_password** de [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) e [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)) devem ser as mesmas que a conta e a senha usadas para a conexão com o Publicador Oracle.  
  
    -   Você não pode alterar o parâmetro **@job_login** por meio de [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) ou [sp_changelogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md), mas a senha pode ser alterada.  
  
 Para mais informações sobre segurança de replicação, consulte [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações administrativas sobre Publicadores Oracle](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
