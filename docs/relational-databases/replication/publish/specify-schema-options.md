---
title: "Especificar op&#231;&#245;es de esquema | Microsoft Docs"
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
  - "esquemas [replicação do SQL Server], opções"
  - "artigos [replicação do SQL Server], opções de replicação transacional"
  - "artigos [replicação do SQL Server], opções de replicação de mesclagem"
  - "artigos [replicação do SQL Server], opções de esquema"
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Especificar op&#231;&#245;es de esquema
  Este tópico descreve como especificar opções de esquema no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Ao publicar uma tabela ou exibição, você pode controlar as opções de criação de objeto que são replicadas para o objeto publicado. Você pode definir esta opção quando o artigo é criado, e você também pode alterá-los mais tarde. Se você não especificar essas opções explicitamente para um artigo, um conjunto padrão de opções será definido.  
  
> [!NOTE]  
>  As opções de esquema padrão ao usar procedimentos armazenados de replicação podem diferir das opções padrão quando forem adicionados artigos usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar opções de esquema, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Para alterar opções de esquema após a criação da publicação, gere um novo instantâneo.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Para obter a lista completa de opções de esquema, consulte o **@schema_option** parâmetro [sp_addarticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especificar opções de esquema, como copiar restrições e gatilhos para assinantes, no **propriedades** guia de **Propriedades do artigo - \< artigo>** caixa de diálogo. Essa guia está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar opções de esquema  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um artigo e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Selecione quais alterações de opção de esquema de artigos devem ser aplicar a:  
  
    -   Clique em **definir propriedades de realçado \< ObjectType> artigo** para iniciar o **Propriedades do artigo - \< ObjectName>** caixa de diálogo; propriedade as alterações feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel do objeto no **artigos** página.  
  
    -   Clique em **definir propriedades de todos os \< ObjectType> artigos** para iniciar o **Propriedades para todos os \< ObjectType> artigos** caixa de diálogo; propriedade as alterações feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo no painel objeto o **artigos** página, incluindo os ainda não foram selecionados para publicação.  
  
        > [!NOTE]  
        >  Alterações de propriedade feitas a **Propriedades para todos os \< ObjectType> artigos** caixa de diálogo Substituir qualquer feitas anteriormente no **Propriedades do artigo - \< ObjectName>** caixa de diálogo. Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
3.  No **copiar objetos e configurações no assinante** e **objeto de destino** seções o **propriedades** Guia do **Propriedades do artigo - \< artigo>** caixa de diálogo, especifique valores para as opções.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
5.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Opções de esquema são especificadas como um valor hexadecimal de [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) resultado de uma ou mais opções. Para obter mais informações, consulte [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
> [!NOTE]  
>  Você deve converter valores de opção de esquema de **binary** para **int** antes de executar uma operação bit a bit. Para obter mais informações, consulte [CAST e CONVERT & #40. O Transact-SQL e 41;](../../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
#### Para especificar opções de esquema ao definir um artigo para uma publicação de instantâneo ou transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, o tipo de objeto de banco de dados para **@type**, e o [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) resultado de uma ou mais opções de esquema para **@schema_option**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para especificar opções de esquema ao definir um artigo para uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, e o [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) resultado de uma ou mais opções de esquema para **@schema_option**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para alterar opções de esquema para um artigo existente em uma publicação de instantâneo ou transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication** e o nome do artigo para **@article**. Observe o valor da **schema_option** coluna no conjunto de resultados.  
  
2.  Executar um [& (e bit a bit)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) valor para determinar se a opção está definida de opção de operação usando o valor da etapa 1 e o esquema desejado.  
  
    -   Se o resultado for **0**, a opção não está definida.  
  
    -   Se o resultado for o valor da opção, a opção já está definida.  
  
3.  Se a opção não for definida, execute um [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) operação usando o valor da etapa 1 e o valor de opção de esquema desejado.  
  
4.  No publicador do banco de dados de publicação, execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, o nome do artigo para **@article**, um valor de **schema_option** para **@property**, e o resultado hexadecimal da etapa 3 para **@value**.  
  
5.  Execute o Agente de Instantâneo para gerar um novo instantâneo. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### Para alterar opções de esquema para um artigo existente em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication** e o nome do artigo para **@article**. Observe o valor da **schema_option** coluna no conjunto de resultados.  
  
2.  Executar um [& (e bit a bit)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) valor para determinar se a opção está definida de opção de operação usando o valor da etapa 1 e o esquema desejado.  
  
    -   Se o resultado for **0**, a opção não está definida.  
  
    -   Se o resultado for o valor da opção, a opção já está definida.  
  
3.  Se a opção não for definida, execute um [| (OR bit a bit)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) operação usando o valor da etapa 1 e o valor de opção de esquema desejado.  
  
4.  No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, o nome do artigo para **@article**, um valor de **schema_option** para **@property**, e o resultado hexadecimal da etapa 3 para **@value**.  
  
5.  Execute o Agente de Instantâneo para gerar um novo instantâneo. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## Consulte também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Opções de artigo para replicação transacional](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  