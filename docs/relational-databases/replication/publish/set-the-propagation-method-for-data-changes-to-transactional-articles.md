---
title: "Definir o m&#233;todo de propaga&#231;&#227;o de altera&#231;&#245;es de dados para artigos transacionais | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "transactional replication, propagation methods"
  - "propagando alterações de dados [replicação do SQL Server]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Definir o m&#233;todo de propaga&#231;&#227;o de altera&#231;&#245;es de dados para artigos transacionais
  Este tópico descreve como definir o método de propagação para alterações de dados para artigos transacionais no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Por padrão, a replicação transacional propaga alterações para os Assinantes usando um conjunto de procedimentos armazenados para cada um dos artigos. É possível substituir esses procedimentos por procedimentos personalizados. Para obter mais informações, consulte [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir o método de propagação de alterações de dados para artigos transacionais, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   É preciso tomar cuidado ao editar qualquer um dos arquivos de instantâneo gerados pela replicação. Você deve testar e oferecer suporte à lógica personalizada nos procedimentos armazenados personalizados. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] não oferece suporte à lógica personalizada.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especificar o método de propagação no **propriedades** guia o **Propriedades do artigo - \< artigo>** caixa de diálogo, que está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar o método de propagação  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
3.  No **propriedades** Guia do **Propriedades do artigo - \< artigo>** na caixa de **entrega de instrução** especifique o método de propagação para cada operação usando o **formato de entrega de inserção**, **formato de entrega de atualização**, e **formato de entrega de exclusão** menus.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para gerar e usar procedimentos armazenados personalizados  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela e, em seguida, clique em **Propriedades do artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
     No **propriedades** Guia do **Propriedades do artigo - \< artigo>** na caixa a **entrega de instrução** seção, selecione a sintaxe de chamada no menu formato de entrega apropriado (**formato de entrega INSERT**, **formato de entrega de atualização**, ou **formato de entrega DELETE**) e, em seguida, digite o nome do procedimento para usar em **procedimento armazenado INSERT**, **Excluir procedimento armazenado**, ou **procedimento armazenado de atualização**. Para obter mais informações sobre a sintaxe de chamada, consulte a seção "Sintaxe de chamada de procedimentos armazenados" em [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
5.  Quando o instantâneo para a publicação for gerado, incluirá o procedimento especificado na etapa anterior. Os procedimentos usarão a sintaxe CALL especificada, mas incluirão a lógica padrão utilizada pela replicação.  
  
     Após a geração do instantâneo, vá até a pasta do instantâneo da publicação à qual esse artigo pertence e localize o arquivo **.sch** com nome idêntico ao do artigo. Abra esse arquivo usando o Bloco de Notas ou outro editor de textos, localize o comando CREATE PROCEDURE para os procedimentos de inserir, atualizar ou excluir e edite a definição do procedimento para fornecer todas as lógicas de personalização para a propagação das alterações de dados. Se o instantâneo for regenerado, será preciso recriar o procedimento personalizado.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 A replicação transacional permite que você controle como as alterações são propagadas do Publicador para os Assinantes, e esse método de propagação pode ser definido programaticamente quando um artigo é criado e posteriormente alterado usando procedimentos armazenados de replicação.  
  
> [!NOTE]  
>  Você pode especificar um método de propagação diferente para cada tipo de operação DML (linguagem de manipulação de dados) - inserir, atualizar ou deletar - que ocorra em uma linha de um dado publicado.  
  
 Para obter mais informações, consulte [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Para criar um artigo que use comandos Transact-SQL para propagar alterações de dados  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, e um valor de **SQL** para pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** -controla a replicação do [Inserir](../../../t-sql/statements/insert-transact-sql.md) comandos.  
  
    -   **@upd_cmd** -controla a replicação do [atualização](../../../t-sql/queries/update-transact-sql.md) comandos.  
  
    -   **@del_cmd** -controla a replicação do [Excluir](../../../t-sql/statements/delete-transact-sql.md) comandos.  
  
    > [!NOTE]  
    >  Ao especificar um valor de **SQL** para qualquer um dos parâmetros acima, comandos desse tipo serão replicados para o assinante como apropriado [!INCLUDE[tsql](../../../includes/tsql-md.md)] comando.  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para criar um artigo que não propague alterações de dados  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, e um valor de **NONE** para pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** -controla a replicação do [Inserir](../../../t-sql/statements/insert-transact-sql.md) comandos.  
  
    -   **@upd_cmd** -controla a replicação do [atualização](../../../t-sql/queries/update-transact-sql.md) comandos.  
  
    -   **@del_cmd** -controla a replicação do [Excluir](../../../t-sql/statements/delete-transact-sql.md) comandos.  
  
    > [!NOTE]  
    >  Ao especificar um valor de **NONE** para qualquer um dos parâmetros acima, os comandos desse tipo não serão replicados para o assinante.  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para criar um artigo com procedimentos armazenados personalizados modificados pelo usuário  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, um valor para o **@schema_option** bitmask que contém o valor **0x02** (permite a geração automática de procedimentos armazenados personalizados) e pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** -Especifique um valor de **CALL sp_msins _*article_name***, onde ***article_name*** é o valor especificado para **@article**.  
  
    -   **@del_cmd** -Especifique um valor de **sp_msdel _ chamada*article_name*** ou **XCALL sp_msdel _*article_name***, onde ***article_name*** é o valor especificado para **@article**.  
  
    -   **@upd_cmd** -Especifique um valor de **SCALL sp_msupd _*article_name***, **sp_msupd _ chamada*article_name***, **sp_msupd _ XCALL*article_name***, ou **sp_msupd _ MCALL*article_name***, onde ***article_name*** é o valor especificado para **@article**.  
  
    > [!NOTE]  
    >  Para cada um dos parâmetros de comando acima, você pode especificar seu próprio nome para os procedimentos armazenados que a replicação gera.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre a sintaxe de chamada, SCALL, XCALL e MCALL, consulte [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Após a geração do instantâneo, vá até a pasta do instantâneo da publicação à qual esse artigo pertence e localize o arquivo **.sch** com nome idêntico ao do artigo. Abra esse arquivo usando Notepad.exe, localize o comando CREATE PROCEDURE para os procedimentos armazenados de inserir, atualizar ou excluir, e edite a definição do procedimento para fornecer as lógicas de personalização para a propagação das alterações de dados. Para obter mais informações, consulte [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Para criar um artigo com script personalizado nos procedimentos armazenados personalizados para propagar alterações de dados  
  
1.  No publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication**, um nome para o artigo para **@article**, o objeto de banco de dados que está sendo publicado para **@source_object**, um valor para o **@schema_option** bitmask que contém o valor **0x02** (permite a geração automática de procedimentos armazenados personalizados) e pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** -Especifique um valor de **CALL sp_msins _*article_name***, onde ***article_name*** é o valor especificado para **@article**.  
  
    -   **@del_cmd** -Especifique um valor de **sp_msdel _ chamada*article_name*** ou **XCALL sp_msdel _*article_name***, onde ***article_name*** é o valor especificado para **@article**.  
  
    -   **@upd_cmd** -Especifique um valor de **SCALL sp_msupd _*article_name***, **sp_msupd _ chamada*article_name***, **sp_msupd _ XCALL*article_name***, **sp_msupd _ MCALL*article_name***, onde ***article_name*** é o valor especificado para **@article**.  
  
    > [!NOTE]  
    >  Para cada um dos parâmetros de comando acima, você pode especificar seu próprio nome para os procedimentos armazenados que a replicação gera.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre a sintaxe de chamada, SCALL, XCALL e MCALL, consulte [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  No publicador do banco de dados de publicação, use o [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) instrução editar [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) para que ele retorne um [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) script para o insert, update e delete personalizados armazenado procedimentos. Para obter mais informações, consulte [especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Para alterar o método de propagar alterações para um artigo existente  
  
1.  No publicador do banco de dados de publicação, execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Especifique **@publication**, **@article**, um valor de **ins_cmd**, **upd_cmd**, ou **del_cmd** para **@property**, e o método de propagação apropriado para **@value**.  
  
2.  Repita a etapa 1 para cada método de propagação a ser alterado.  
  
## Consulte também  
 [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [Criar, modificar e excluir publicações e artigos e 40; Replicação e 41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  