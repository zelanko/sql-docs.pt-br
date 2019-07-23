---
title: Definir o método de propagação de alterações de dados para artigos transacionais | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 969012ebc2cb804fe67cfb04810d653eb8041f52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073487"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>Definir o método de propagação de alterações de dados para artigos transacionais
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como definir o método de propagação para alterações de dados para artigos transacionais no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Por padrão, a replicação transacional propaga alterações para os Assinantes usando um conjunto de procedimentos armazenados para cada um dos artigos. É possível substituir esses procedimentos por procedimentos personalizados. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir o método de propagação de alterações de dados para artigos transacionais, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   É preciso tomar cuidado ao editar qualquer um dos arquivos de instantâneo gerados pela replicação. Você deve testar e oferecer suporte à lógica personalizada nos procedimentos armazenados personalizados. A[!INCLUDE[msCoName](../../../includes/msconame-md.md)] não oferece suporte à lógica personalizada.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique o método de propagação na guia **Propriedades** da caixa de diálogo **Propriedades do artigo – \<Artigo>** , que está disponível no Assistente para Nova Publicação e a caixa de diálogo **Propriedades da publicação – \<Publicação>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-the-propagation-method"></a>Para especificar o método de propagação  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
3.  Na guia **Propriedades**, da caixa de diálogo **Propriedades do artigo – \<Artigo>** na seção **Entrega de Instrução**, especifique o método de propagação para cada operação usando os menus **Formato de entrega de INSERT**, **Formato de entrega de UPDATE** e **Formato de entrega de DELETE**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="to-generate-and-use-custom-stored-procedures"></a>Para gerar e usar procedimentos armazenados personalizados  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir as Propriedades do Artigo Realçado da Tabela**.  
  
     Na guia **Propriedades**, da caixa de diálogo **Propriedades do Artigo – \<Artigo>** , na seção **Entrega de Instrução**, selecione a sintaxe CALL no menu de formato de entrega apropriado (**Formato de entrega de INSERT**, **Formato de entrega de UPDATE** ou **Formato de entrega de DELETE**), depois digite o nome do procedimento a ser usado no **Procedimento armazenado INSERT**, **Procedimento armazenado DELETE** ou **Procedimento armazenado UPDATE**. Para obter mais informações sobre a sintaxe de chamada, consulte a seção “Sintaxe de chamada de procedimentos armazenados” em [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
5.  Quando o instantâneo para a publicação for gerado, incluirá o procedimento especificado na etapa anterior. Os procedimentos usarão a sintaxe CALL especificada, mas incluirão a lógica padrão utilizada pela replicação.  
  
     Após a geração do instantâneo, vá até a pasta do instantâneo da publicação à qual esse artigo pertence e localize o arquivo **.sch** com nome idêntico ao do artigo. Abra esse arquivo usando o Bloco de Notas ou outro editor de textos, localize o comando CREATE PROCEDURE para os procedimentos de inserir, atualizar ou excluir e edite a definição do procedimento para fornecer todas as lógicas de personalização para a propagação das alterações de dados. Se o instantâneo for regenerado, será preciso recriar o procedimento personalizado.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 A replicação transacional permite que você controle como as alterações são propagadas do Publicador para os Assinantes, e esse método de propagação pode ser definido programaticamente quando um artigo é criado e posteriormente alterado usando procedimentos armazenados de replicação.  
  
> [!NOTE]  
>  Você pode especificar um método de propagação diferente para cada tipo de operação DML (linguagem de manipulação de dados) - inserir, atualizar ou deletar - que ocorra em uma linha de um dado publicado.  
  
 Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>Para criar um artigo que use comandos Transact-SQL para propagar alterações de dados  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication** , um nome para o artigo para **@article** , o objeto de banco de dados a ser publicado para **@source_object** e um valor de **SQL** para pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** - controla a replicação dos comandos [INSERT](../../../t-sql/statements/insert-transact-sql.md) .  
  
    -   **@upd_cmd** - controla a replicação dos comandos [UPDATE](../../../t-sql/queries/update-transact-sql.md) .  
  
    -   **@del_cmd** - controla a replicação dos comandos [DELETE](../../../t-sql/statements/delete-transact-sql.md) .  
  
    > [!NOTE]  
    >  Ao especificar um valor de **SQL** para qualquer um dos parâmetros acima, os comandos desse tipo serão replicados para o Assinante como o comando [!INCLUDE[tsql](../../../includes/tsql-md.md)] apropriado.  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>Para criar um artigo que não propague alterações de dados  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication** , um nome para o artigo para **@article** , o objeto de banco de dados a ser publicado para **@source_object** e um valor de **NONE** para pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** - controla a replicação dos comandos [INSERT](../../../t-sql/statements/insert-transact-sql.md) .  
  
    -   **@upd_cmd** - controla a replicação dos comandos [UPDATE](../../../t-sql/queries/update-transact-sql.md) .  
  
    -   **@del_cmd** - controla a replicação dos comandos [DELETE](../../../t-sql/statements/delete-transact-sql.md) .  
  
    > [!NOTE]  
    >  Ao especificar um valor de **NONE** para qualquer um dos parâmetros acima, os comandos desse tipo não serão replicados para o Assinante.  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>Para criar um artigo com procedimentos armazenados personalizados modificados pelo usuário  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication** , um nome para o artigo para **@article** , o objeto de banco de dados a ser publicado para **@source_object** , um valor para o bitmask **@schema_option** que contém o valor **0x02** (habilita geração automática de procedimentos armazenados personalizados) e pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** – especificar um valor de **CALL sp_MSins_* article_name***, em que ***article_name*** é o valor especificado para **@article** .  
  
    -   **@del_cmd** – especificar um valor de **CALL sp_MSdel_*article_name*** ou **XCALL sp_MSdel_* article_name***, em que ***article_name*** é o valor especificado para **@article** .  
  
    -   **@upd_cmd** – especificar um valor de **SCALL sp_MSupd_* article_name***, **CALL sp_MSupd_* article_name***, **XCALL sp_MSupd_* article_name*** ou **MCALL sp_MSupd_* article_name***, em que ***article_name*** é o valor especificado para **@article** .  
  
    > [!NOTE]  
    >  Para cada um dos parâmetros de comando acima, você pode especificar seu próprio nome para os procedimentos armazenados que a replicação gera.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre a sintaxe de CALL, SCALL, XCALL e MCALL, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Após a geração do instantâneo, vá até a pasta do instantâneo da publicação à qual esse artigo pertence e localize o arquivo **.sch** com nome idêntico ao do artigo. Abra esse arquivo usando Notepad.exe, localize o comando CREATE PROCEDURE para os procedimentos armazenados de inserir, atualizar ou excluir, e edite a definição do procedimento para fornecer as lógicas de personalização para a propagação das alterações de dados. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>Para criar um artigo com script personalizado nos procedimentos armazenados personalizados para propagar alterações de dados  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para **@publication** , um nome para o artigo para **@article** , o objeto de banco de dados a ser publicado para **@source_object** , um valor para o bitmask **@schema_option** que contém o valor **0x02** (habilita geração automática de procedimentos armazenados personalizados) e pelo menos um dos seguintes parâmetros:  
  
    -   **@ins_cmd** – especificar um valor de **CALL sp_MSins_* article_name***, em que ***article_name*** é o valor especificado para **@article** .  
  
    -   **@del_cmd** – especificar um valor de **CALL sp_MSdel_*article_name*** ou **XCALL sp_MSdel_* article_name***, em que ***article_name*** é o valor especificado para **@article** .  
  
    -   **@upd_cmd** – especificar um valor de **SCALL sp_MSupd_* article_name***, **CALL sp_MSupd_* article_name***, **XCALL sp_MSupd_* article_name***, **MCALL sp_MSupd_* article_name***, em que ***article_name*** é o valor especificado para **@article** .  
  
    > [!NOTE]  
    >  Para cada um dos parâmetros de comando acima, você pode especificar seu próprio nome para os procedimentos armazenados que a replicação gera.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre a sintaxe de CALL, SCALL, XCALL e MCALL, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  No Publicador do banco de dados de publicação, use a instrução [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) para editar [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) de maneira que retorne um script [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) para os procedimentos armazenados personalizados de inserir, atualizar e deletar. Para obter mais informações, consulte [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>Para alterar o método de propagar alterações para um artigo existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Especifique **@publication** , **@article** , um valor de **ins_cmd**, **upd_cmd**ou **del_cmd** para **@property** e o método de propagação apropriado para **@value** .  
  
2.  Repita a etapa 1 para cada método de propagação a ser alterado.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar como as alterações são propagadas para artigos transacionais](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  
