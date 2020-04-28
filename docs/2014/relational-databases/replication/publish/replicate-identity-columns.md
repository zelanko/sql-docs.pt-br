---
title: Replicar colunas de identidade | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identities [SQL Server replication]
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7c6410e6b21ec3ebbb3cfb01fa78ffe80b2196a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74479249"
---
# <a name="replicate-identity-columns"></a>Replicar colunas de identidade
  Quando se atribui uma propriedade IDENTITY a uma coluna, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gera automaticamente números sequenciais para novas linhas inseridas na tabela que contém a coluna de identidade. Para obter mais informações, consulte [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property). Como as colunas de identidade podem ser incluídas como parte da chave primária, é importante evitar valores duplicados nas colunas de identidade. Para que colunas de identidade sejam usadas em uma topologia de replicação que tenha atualizações em mais de um nó, cada nó da topologia de replicação precisará usar um intervalo diferente de valores de identidade, de modo que não ocorram duplicatas.  
  
 Por exemplo, o intervalo de 1 a 100 poderia ser atribuído ao Publicador; o intervalo de 101 a 200 ao Assinante A e o intervalo de 201 a 300 ao Assinante B. Se uma linha for inserida no Publicador e o valor de identidade for, por exemplo, 65, esse valor será replicado para cada Assinante. Quando a replicação insere dados em cada Assinante, isso não incrementa o valor da coluna de identidade na tabela Assinante. Em vez disso, o valor literal 65 é inserido. Somente as inserções do usuário, não as inserções do agente de replicação, causam o incremento da coluna de identidade.  
  
 A replicação trata colunas de identidade em todos os tipos de publicação e assinatura, o que permite gerenciar as colunas manualmente ou fazer com que a replicação as gerencie de forma automática.  
  
> [!NOTE]  
>  Não há suporte para adicionar uma coluna de identidade a uma tabela publicada, pois isso pode resultar em não convergência quando a coluna é replicada no Assinante. Os valores na coluna de identidade no Publicador dependerão da ordem em que as linhas para a tabela afetada forem armazenadas fisicamente. As linhas podem ser armazenadas de forma diversa no Assinante; assim, o valor da coluna de identidade pode ser diferente para as mesmas linhas.  
  
## <a name="specifying-an-identity-range-management-option"></a>Especificando uma opção de gerenciamento de intervalo de identidade  
 A replicação oferece três opções de gerenciamento de intervalo de identidade:  
  
-   Automático. Usado para replicação de mesclagem e replicação transacional com atualizações do Assinante. Especifique os intervalos de tamanho para o Publicador e para os Assinantes, e a replicação gerenciará automaticamente a atribuição de novos intervalos. A replicação define a opção NOT FOR REPLICATION na coluna de identidade do Assinante, de modo que somente as inserções do usuário geram o valor a ser incrementado no Assinante.  
  
    > [!NOTE]  
    >  Para que novos intervalos sejam recebidos é preciso que haja sincronização entre os Assinantes e o Publicador. Como os intervalos de identidade são atribuídos automaticamente aos Assinantes, é possível que qualquer Assinante esgote todo o fornecimento de intervalos de identidade quando novos intervalos são solicitados repetidamente.  
  
-   Manual. Usado para replicação de instantâneo e transacional sem atualizações no Assinante, replicação transacional ponto a ponto ou quando é necessário que o aplicativo controle de forma programática os intervalos de identidade. Se o gerenciamento manual for especificado, será preciso assegurar que intervalos sejam atribuídos ao Publicador e a cada Assinante e que novos intervalos sejam atribuídos, caso os intervalos iniciais sejam utilizados. A replicação define a opção NOT FOR REPLICATION na coluna de identidade do Assinante.  
  
-   Nenhum. Essa opção é recomendada apenas para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , sendo disponibilizada apenas na interface do procedimento armazenado para as publicações transacionais.  
  
 Para especificar uma opção de gerenciamento de intervalos de identidade, consulte [Gerenciar colunas de identidade](manage-identity-columns.md).  
  
## <a name="assigning-identity-ranges"></a>Atribuindo intervalos de identidade  
 A replicação de mesclagem e a replicação transacional usam diferentes métodos para a atribuição de intervalos. Esses métodos são descritos nesta seção.  
  
 Há dois tipos de intervalos a serem considerados quando se replicam colunas de identidade: os intervalos atribuídos ao Publicador e Assinantes, e o intervalo do tipo de dados na coluna. A tabela a seguir mostra os intervalos disponíveis para os tipos de dados usados normalmente em colunas de identidade. O intervalo é usado em todos os nós de uma topologia. Por exemplo, se você usar `smallint` a partir de 1 com um incremento de 1, o número máximo de inserções será 32.767 para o Publicador e todos os assinantes. O número real de inserções depende da existência de lacunas nos valores usados e da utilização de um valor limite. Para obter mais informações sobre limites, consulte as seções a seguir, "Replicação de mesclagem" e "Replicação transacional com assinaturas de atualização enfileirada".  
  
 Se o Publicador esgotar seu intervalo de identidade após uma inserção, ele poderá atribuir um novo intervalo se a inserção tiver sido realizada por um membro de uma função de banco de dados fixa **db_owner** . Se a inserção tiver sido realizada por um usuário que não estava nessa função, o Agente de Leitor de Log, o Agente de Mesclagem ou um usuário que é membro da função **db_owner** deverá executar [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql). Para publicações transacionais, o Agente de Leitor de Log deverá estar em execução para alocar automaticamente um novo intervalo (o padrão é que o agente seja executado continuamente).  
  
> [!WARNING]  
>  Durante uma inserção de lote grande, o gatilho de replicação é disparado apenas uma vez, e não para cada linha da inserção. Isso pode resultar em falha na instrução de inserção se um intervalo de identidade for esgotado durante uma inserção grande, como a instrução `INSERT INTO`.  
  
|Tipo de dados|Intervalo|  
|---------------|-----------|  
|`tinyint`|Não tem suporte para gerenciamento automático|  
|`smallint`|-2^15 (-32.768) a 2^15-1 (32.767)|  
|`int`|-2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647)|  
|`bigint`|-2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807)|  
|`decimal` e `numeric`|-10^38+1 até 10^38-1|  
  
> [!NOTE]  
>  Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../../sequence-numbers/sequence-numbers.md).  
  
### <a name="merge-replication"></a>Replicação de mesclagem  
 Os intervalos de identidade são gerenciados pelo Publicador e propagados para os Assinantes pelo Merge Agent (em uma hierarquia de republicação, os intervalos são gerenciados pelo Publicador raiz e pelos republicadores). Os valores de identidade são atribuídos em um pool do Publicador. Ao adicionar um artigo com uma coluna de identidade a uma publicação no Assistente para Nova Publicação ou ao usar [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), especifique valores para:  
  
-   O ** \@parâmetro identity_range** , que controla o tamanho do intervalo de identidade inicialmente alocado para o Publicador e para assinantes com assinaturas de cliente.  
  
    > [!NOTE]  
    >  Para assinantes que executam [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]versões anteriores do, esse parâmetro (em vez do ** \@parâmetro pub_identity_range** ) também controla o tamanho do intervalo de identidade em assinantes de republicação.  
  
-   O ** \@parâmetro pub_identity_range** , que controla o tamanho do intervalo de identidade para republicação alocada para assinantes com assinaturas de servidor (necessárias para republicação de dados). Todos os Assinantes com assinaturas de servidor recebem um intervalo para republicar, mesmo se eles de fato não republiquem dados.  
  
-   O ** \@parâmetro Threshold** , que é usado para determinar quando um novo intervalo de identidades é necessário para uma assinatura [!INCLUDE[ssEW](../../../includes/ssew-md.md)] do ou para uma versão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]anterior do.  
  
 Por exemplo, você pode especificar 10000 para ** \@identity_range** e 500000 para ** \@pub_identity_range**. Um intervalo primário de 10.000 é atribuído ao Publicador e a todos os Assinantes que executam o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior, inclusive ao Assinante com a assinatura do servidor. O Assinante com a assinatura do servidor também é atribuído a um intervalo primário de 500000, que pode ser usado por assinantes que sincronizam com o Assinante de republicação (você também deve especificar ** \@identity_range**, ** \@pub_identity_range**e ** \@limite** para os artigos na publicação no Assinante de republicação).  
  
 Todo Assinante que executa o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou uma versão posterior também recebe um intervalo de identidade secundário. O intervalo secundário é igual em tamanho ao intervalo primário. Quando o intervalo primário se esgota, o intervalo secundário é usado, e o Merge Agent atribui um novo intervalo ao Assinante. O novo intervalo passa a ser o intervalo secundário, e o processo continua à medida que o Assinante utiliza valores de identidade.  
  
  
### <a name="transactional-replication-with-queued-updating-subscriptions"></a>Replicação transacional com assinaturas de atualização enfileirada  
 Os intervalos de identidade são gerenciados pelo Distribuidor e propagados para os Assinantes pelo Distribution Agent. Os valores de identidade são atribuídos em um pool do Distribuidor. O tamanho do pool baseia-se no tamanho dos tipos de dados e no incremento usado para a coluna de identidade. Ao adicionar um artigo com uma coluna de identidade a uma publicação no Assistente para Nova Publicação ou ao usar [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql), especifique valores para:  
  
-   O ** \@parâmetro identity_range** , que controla o tamanho do intervalo de identidade inicialmente alocado para todos os assinantes.  
  
-   O ** \@parâmetro pub_identity_range** , que controla o tamanho do intervalo de identidade alocado para o Publicador.  
  
-   O ** \@parâmetro Threshold** , que é usado para determinar quando um novo intervalo de identidades é necessário para uma assinatura.  
  
 Por exemplo, você pode especificar 10000 para ** \@pub_identity_range**, 1000 para ** \@identity_range** (supondo menos atualizações no Assinante) e 80% para ** \@o limite**. Após 800 inserções em um Assinante (80 por cento de 1.000), um Assinante é atribuído a um novo intervalo. Depois de 8.000 inserções em um Publicador, um novo intervalo é atribuído ao Publicador. Quando o novo intervalo é atribuído, há uma lacuna nos valores de intervalo de identidade da tabela. Especificar um limite superior resulta em lacunas menores, mas o sistema torna-se menos tolerante a falhas. Se o Merge Agent não puder ser executado por algum motivo, um Assinante poderá ficar mais facilmente sem identidades.  
  
## <a name="assigning-ranges-for-manual-identity-range-management"></a>Atribuindo intervalos para o gerenciamento manual de intervalo de identidade  
 Caso o gerenciamento manual de identidade seja especificado, será preciso assegurar que o Publicador e cada um dos Assinantes usem intervalos de identidade diferentes. Por exemplo, considere uma tabela do Publicador com coluna de identidade definida como `IDENTITY(1,1)`: a coluna de identidade começa com 1 e é incrementada em 1 toda vez que uma linha é inserida. Se a tabela do Publicador tiver 5.000 linhas, e houver expectativa de algum aumento da tabela durante a vida útil do aplicativo, o Publicador poderá usar o intervalo de 1 a 10.000. Considerando-se dois Assinantes, o Assinante A poderá usar de 10.001 a 20.000 e o Assinante B poderá usar de 20.001 a 30.000.  
  
 Após o Assinante ser iniciado com um instantâneo ou por outros meios, execute DBCC CHECKIDENT para atribuir ao Assinante um ponto inicial para o seu intervalo de identidade. Por exemplo, no Assinante A, `DBCC CHECKIDENT('<TableName>','reseed',10001)`seria executado. No Assinante B, `CHECKIDENT('<TableName>','reseed',20001)`seria executado.  
  
 Para atribuir novos intervalos ao Publicador ou aos Assinantes, execute DBCC CHECKIDENT e especifique um novo valor para semear novamente a tabela. Deve haver algum modo de determinar quando um novo intervalo precisa ser atribuído. Por exemplo, o aplicativo pode ter um mecanismo que detecte quando um nó está prestes a esgotar seu intervalo e a atribuir um novo intervalo usando DBCC CHECKIDENT. Você também pode adicionar uma restrição de verificação para assegurar que não seja possível adicionar uma linha caso ela possa causar o uso de um valor de identidade fora do intervalo.  
  
## <a name="handling-identity-ranges-after-a-database-restore"></a>Tratando intervalos de identidade após uma restauração de banco de dados  
 Caso o gerenciamento de identidade automático seja utilizado, quando um Assinante for restaurado de um backup, ele solicitará automaticamente um novo intervalo de valores de identidade. Se um Publicador for restaurado de um backup, assegure que um intervalo adequado seja atribuído ao Publicador. Para a replicação de mesclagem, atribua um novo intervalo usando [sp_restoremergeidentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql). Para a replicação transacional, determine o valor mais alto que foi utilizado; em seguida, defina o ponto inicial para os novos intervalos. Use o procedimento a seguir depois que o banco de dados de publicação tiver sido restaurado:  
  
1.  Pare toda a atividade em todos os Assinantes.  
  
2.  Para cada tabela publicada que inclua uma coluna de identidade:  
  
    1.  No banco de dados de assinatura de cada Assinante, execute `IDENT_CURRENT('<TableName>')`.  
  
    2.  Registre o valor mais alto encontrado em todos os Assinantes.  
  
    3.  No banco de dados de publicação do Publicador, execute `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`).  
  
    4.  No banco de dados de publicação do Publicador, execute `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`.  
  
    > [!NOTE]  
    >  Se o valor da coluna identidade estiver definido para redução em vez de incremento, registre o valor mais baixo encontrado, depois semeie novamente esse valor.  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [&#41;&#40;Transact-SQL de DBCC CHECKIDENT](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)   
 [&#41;&#40;Transact-SQL de IDENT_CURRENT](/sql/t-sql/functions/ident-current-transact-sql)   
 [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)   
 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql)  
  
  
