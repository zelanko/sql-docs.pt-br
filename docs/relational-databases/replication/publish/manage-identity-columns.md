---
title: "Gerenciar colunas de identidade | Microsoft Docs"
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
  - "valores de identidade [replicação do SQL Server]"
  - "replicação de mesclagem [replicação do SQL Server], gerenciamento de intervalo de identidades"
  - "publicação [replicação do SQL Server], colunas de identidade"
  - "replicação transacional, gerenciamento de intervalo de identidades"
  - "colunas de identidade [SQL Server], replicação"
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Gerenciar colunas de identidade
  Este tópico descreve como gerenciar colunas de identidade no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Quando as inserções de Assinante são replicadas de volta ao Publicador, as colunas de identidade devem ser gerenciadas para evitar a atribuição do mesmo valor de identidade para o Assinante e o Publicador. A Replicação pode gerenciar intervalos de identidade automaticamente ou você pode escolher controlar o gerenciamento de intervalo de identidade manualmente.  Para obter informações sobre as opções de gerenciamento de intervalo de identidade fornecidas pela replicação, consulte [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para gerenciar colunas de identidade, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Ao publicar uma tabela em mais de uma publicação, você deve especificar as mesmas opções de gerenciamento do intervalo da identidade para ambas a publicações. Para obter mais informações, consulte "Publicando tabelas em mais de uma publicação" em [publica dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
-   Para criar um número incrementado automaticamente, que pode ser usado em várias tabelas ou que pode ser chamado de aplicativos sem referenciar qualquer tabela, consulte [números de sequência](../../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especificar uma opção de gerenciamento de coluna de identidade no **propriedades** guia o **Propriedades do artigo - \< artigo>** caixa de diálogo do Assistente de nova publicação. Para obter mais informações sobre como usar esse assistente, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md). No Assistente para Nova Publicação:  
  
-   Se você selecionar **publicação de mesclagem** ou **publicação transacional com assinaturas de atualização** sobre o **tipo de publicação** selecione gerenciamento de intervalo de identidade automática ou manual (automático, o padrão, é recomendado). Depois que a tabela é publicada, a propriedade não pode ser modificada, mas outras propriedades relacionadas a ela, sim.  
  
-   Se você selecionar outros tipos de publicação, o gerenciamento de intervalo de identidade deve ser definido como manual.  
  
 Modificar intervalos de identidade e limites no **propriedades** Guia do **Propriedades do artigo - \< artigo>**, que está disponível na **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar uma opção de gerenciamento de coluna de identidade  
  
1.  Se o Publicador estiver executando uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior à [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], na página **Tipo de Publicação** do Assistente para Nova Publicação, selecione **Publicação de mesclagem** ou **Publicação transacional com assinaturas atualizáveis**.  
  
2.  Na página **Artigos** , selecione uma tabela com uma coluna de identidade.  
  
3.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
4.  No **propriedades** Guia do **Propriedades do artigo - \< artigo>** na caixa a **gerenciamento de intervalo de identidade** seção, defina o **Gerenciar automaticamente os intervalos de identidade** propriedade **automática** ou **Manual** (Publicadores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior), ou **True** ou **False** (para Publicadores executando uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]).  
  
5.  Se você selecionou **Automático** ou **Verdadeiro** na etapa 4, digite valores para as opções na tabela a seguir. Para obter mais informações sobre como essas configurações são usadas, consulte a seção "Atribuindo intervalos de identidade" [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
    |Opção|Valor|Descrição|  
    |------------|-----------|-----------------|  
    |**Tamanho do intervalo do Publicador**|Valor inteiro para o tamanho do intervalo (por exemplo, 20000).|Consulte a seção "Atribuindo intervalos de identidade" [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Tamanho do intervalo do assinante**|Valor inteiro para tamanho de intervalo (por exemplo, 10000).|Consulte a seção "Atribuindo intervalos de identidade" [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Porcentagem do limite de intervalo**|Valor inteiro para porcentagem do limite (por exemplo, 90 equivale a 90 por cento).|Porcentagem de valores de identidade totais usados em um nó antes que um novo intervalo de identidade seja atribuído.<br /><br /> <br /><br /> Observação: esse valor deve ser especificado, mas é usado somente por: Assinantes usando assinaturas de atualização enfileiradas, e Assinantes para publicações de mesclagem executando [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ou versões anteriores de outras edições do SQL Server. Para obter mais informações, consulte a seção "Atribuindo intervalos de identidade" [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Valor inicial do intervalo seguinte**|Valor inteiro. Somente leitura.|O valor no qual o próximo intervalo terá início. Por exemplo, se o intervalo atual for 5001-6000, esse valor será 6001.|  
    |**Valor de identidade máximo**|Valor inteiro. Somente leitura.|O valor maior para a coluna de identidade. Determinado pelo tipo de dados base da coluna.|  
    |**Incremento**|Valor inteiro. Somente leitura.|A quantidade pela qual o número na coluna de identidade deve ser aumentado ou diminuído para cada inserção: normalmente definido como 1.|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para modificar intervalos de identidade e limites depois que uma tabela é publicada  
  
1.  Sobre o **artigos** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela com uma coluna de identidade.  
  
2.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
3.  No **propriedades** Guia do **Propriedades do artigo - \< artigo>** na caixa de **gerenciamento de intervalo de identidade** digite valores para uma ou mais das seguintes propriedades: **tamanho do intervalo do publicador**, **tamanho do intervalo do assinante**, e **porcentagem do limite de intervalo**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **OK** sobre o **Propriedades de publicação - \< publicação>** caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Você pode usar os procedimentos armazenados de replicação para especificar as opções de gerenciamento de intervalo da identidade, quando um artigo é criado.  
  
#### Para habilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Se a tabela de origem sendo publicada tiver uma coluna de identidade, especifique um valor de **automática** para **@identityrangemanagementoption**, o intervalo de valores de identidade atribuído ao publicador para **@pub_identity_range**, o intervalo de valores de identidade atribuídos a cada assinantes para **@identity_range**, e a porcentagem total de valores de identidade usadas antes de um novo intervalo de identidade é atribuído para **@threshold**. Para obter mais informações sobre como definir artigos, consulte [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Certifique-se de que os tipos de dados da coluna de identidade é grande o suficiente para oferece suporte a todos os intervalos de identidades atribuídas a todos os Assinantes.  
  
#### Para desabilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique um valor de **manual** para **@ identityrangemanagementoption**. Para obter mais informações sobre como definir artigos, consulte [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Atribua intervalos às colunas de artigo de identidade no Assinante para evitar conflitos ao atualizar Assinantes. Para obter mais informações, consulte a seção sobre Atribuindo intervalos para gerenciamento de intervalo de identidade manual no tópico [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
#### Para habilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Se a tabela de origem sendo publicada tiver uma coluna de identidade, especifique um valor de **automática** para **@identityrangemanagementoption**, o intervalo de valores de identidade atribuído a uma assinatura de servidor para **@pub_identity_range**, o intervalo de valores de identidade atribuído ao publicador e cada assinatura de cliente para **@identity_range**, e a porcentagem total de valores de identidade usadas antes de um novo intervalo de identidade é atribuído para **@threshold**. Para obter mais informações sobre quando novos intervalos de identidade são atribuídos, consulte Atribuindo intervalos de identidade no tópico [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md). Para obter mais informações sobre como definir artigos, consulte [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Certifique-se de que o tipo de dado da coluna de identidade é grande o suficiente para oferece suporte ao intervalo total de identidades atribuídas a todos os Assinantes, especialmente para Assinantes com assinaturas de servidor.  
  
#### Para desabilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique um dos valores a seguir para **@identityrangemanagementoption**:  
  
    -   **manual** -intervalos de identidade devem ser atribuídos manualmente para assinantes de atualização.  
  
    -   **nenhum** -colunas de identidade no publicador não serão definidas como colunas de identidade no assinante.  
  
     Para obter mais informações sobre como definir artigos, consulte [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Atribua intervalos às colunas de artigo de identidade no Assinante para evitar conflitos ao atualizar Assinantes.  
  
#### Para alterar as configurações de gerenciamento de intervalo da identidade para um artigo existente em um instantâneo ou publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) e observe o valor de **identityrangemanagementoption** no conjunto de resultados. Se esse valor for **0**, o gerenciamento de intervalo de identidade automático não estará habilitado.  
  
2.  Se o valor de **identityrangemanagementoption** no conjunto de resultados for **1**, altere as configurações como segue:  
  
    -   Para alterar os intervalos de identidade atribuídos, execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) no publicador do banco de dados de publicação. Especifique um valor de **identity_range** ou **pub_identity_range** para **@property** e o novo valor de intervalo para **@value**.  
  
    -   Para alterar o limite no qual novos intervalos serão atribuídos, execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) no publicador do banco de dados de publicação. Especifique um valor de **threshold** para **@property** e o novo valor de limite para **@value**.  
  
#### Para alterar automaticamente as configurações de gerenciamento de intervalo da identidade para um artigo existente em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) e observe o valor de **identity_support** no conjunto de resultados. Se esse valor for **0**, o gerenciamento de intervalo de identidade automático não estará habilitado.  
  
2.  Se o valor de **identity_support** no conjunto de resultados for **1**, alterar as configurações da seguinte maneira:  
  
    -   Para alterar os intervalos de identidade atribuídos, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) no publicador do banco de dados de publicação. Especifique um valor de **identity_range** ou **pub_identity_range** para **@property** e o novo valor de intervalo para **@value**.  
  
    -   Para alterar o limite no qual novos intervalos serão atribuídos, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) no publicador do banco de dados de publicação. Especifique um valor de **threshold** para **@property** e o novo valor de limite para **@value**. Para obter mais informações sobre quando novos intervalos de identidade são atribuídos, consulte Atribuindo intervalos de identidade no tópico [replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
    -   Para desabilitar o gerenciamento de intervalo de identidade automática, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) no publicador do banco de dados de publicação. Especifique um valor de **identityrangemanagementoption** para **@property** e de **manual** ou **nenhum** para **@value**.  
  
## Consulte também  
 [Replicação transacional ponto a ponto](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Replicar colunas de identidade](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  