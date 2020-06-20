---
title: Especificar opções de esquema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 52064cc189dc62152814436d2d11326a74c89ff6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85005241"
---
# <a name="specify-schema-options"></a>Especificar opções de esquema
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
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Para alterar opções de esquema após a criação da publicação, gere um novo instantâneo.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Para obter a lista completa de opções de esquema, consulte o parâmetro ** \@ schema_option** de [sp_addarticle &#40;&#41;transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) e [sp_addmergearticle &#40;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)&#41;.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique opções de esquema, por exemplo, se deseja copiar restrições e gatilhos para assinantes, na guia **Propriedades** da caixa de diálogo ** \<Article> Propriedades do artigo** . Essa guia está disponível no Assistente para nova publicação e na caixa de diálogo **Propriedades da publicação – \<Publication> ** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-schema-options"></a>Para especificar opções de esquema  
  
1.  Na página **artigos** da caixa de diálogo Assistente para nova publicação ou **Propriedades \<Publication> da publicação –** , selecione um artigo e clique em **Propriedades do artigo**.  
  
2.  Selecione quais alterações de opção de esquema de artigos devem ser aplicar a:  
  
    -   Clique em **definir propriedades do \<ObjectType> artigo realçado** para iniciar as **Propriedades do artigo – \<ObjectName> ** caixa de diálogo; as alterações de propriedade feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel objeto na página **artigos** .  
  
    -   Clique em **definir propriedades de todos os \<ObjectType> artigos** para iniciar a caixa de diálogo **Propriedades de todos os \<ObjectType> artigos** ; as alterações de propriedade feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo no painel de objetos da página **artigos** , incluindo aqueles ainda não selecionados para publicação.  
  
        > [!NOTE]  
        >  As alterações de propriedade feitas na caixa de diálogo **Propriedades de todos os \<ObjectType> artigos** substituem as feitas anteriormente na caixa de diálogo **Propriedades do artigo – \<ObjectName> ** . Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
3.  Nas seções **copiar objetos e configurações para o assinante** e **objeto de destino** da guia **Propriedades** da caixa de diálogo **Propriedades do artigo – \<Article> ** , especifique valores para as opções.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
5.  Se você estiver na caixa de diálogo **Propriedades \<Publication> da publicação –** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As opções de esquema são especificadas como um valor hexadecimal que é o resultado [| (OR bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) de uma ou mais opções. Para obter mais informações, consulte [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) e [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql).  
  
> [!NOTE]  
>  Você deve converter valores de opção de esquema de **binary** para **int** antes de executar uma operação bit a bit. Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>Para especificar opções de esquema ao definir um artigo para uma publicação de instantâneo ou transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação**, um nome para o artigo para o artigo, o objeto de banco de dados que está sendo publicado para ** \@ source_object**, o tipo de objeto de banco de dados para o ** \@ tipo**e o ** \@ ** [| (OR-bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) resultado de uma ou mais opções de esquema para ** \@ schema_option**. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>Para especificar opções de esquema ao definir um artigo para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação**, um nome para o artigo para o ** \@ artigo**, o objeto de banco de dados que está sendo publicado para ** \@ source_object**e [| (OR-bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) resultado de uma ou mais opções de esquema para ** \@ schema_option**. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>Para alterar opções de esquema para um artigo existente em uma publicação de instantâneo ou transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação** e o nome do artigo para o ** \@ artigo**. Observe o valor da coluna **schema_option** no conjunto de resultados.  
  
2.  Execute uma operação [& (AND bit a bit)](/sql/t-sql/language-elements/bitwise-and-transact-sql) usando o valor da etapa 1 e o valor da opção de esquema desejado para determinar se a opção está definida.  
  
    -   Se o resultado for **0**, a opção não está definida.  
  
    -   Se o resultado for o valor da opção, a opção já está definida.  
  
3.  Se a opção não estiver definida, execute uma operação [| (OR de bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) usando o valor da etapa 1 e o valor de opção de esquema desejado.  
  
4.  No Publicador do banco de dados de publicação, execute [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação**, o nome do artigo para o ** \@ artigo**, um valor de **schema_option** para ** \@ Propriedade**e o resultado hexadecimal da etapa 3 para ** \@ valor**.  
  
5.  Execute o Agente de Instantâneo para gerar um novo instantâneo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>Para alterar opções de esquema para um artigo existente em uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação** e o nome do artigo para o ** \@ artigo**. Observe o valor da coluna **schema_option** no conjunto de resultados.  
  
2.  Execute uma operação [& (AND bit a bit)](/sql/t-sql/language-elements/bitwise-and-transact-sql) usando o valor da etapa 1 e o valor da opção de esquema desejado para determinar se a opção está definida.  
  
    -   Se o resultado for **0**, a opção não está definida.  
  
    -   Se o resultado for o valor da opção, a opção já está definida.  
  
3.  Se a opção não estiver definida, execute uma operação [| (OR de bit a bit)](/sql/t-sql/language-elements/bitwise-or-transact-sql) usando o valor da etapa 1 e o valor de opção de esquema desejado.  
  
4.  No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação**, o nome do artigo para o ** \@ artigo**, um valor de **schema_option** para ** \@ Propriedade**e o resultado hexadecimal da etapa 3 para ** \@ valor**.  
  
5.  Execute o Agente de Instantâneo para gerar um novo instantâneo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../create-and-apply-the-initial-snapshot.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)   
 [Article Options for Transactional Replication](../transactional/article-options-for-transactional-replication.md)  
  
  
