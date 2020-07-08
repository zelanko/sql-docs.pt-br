---
title: Implementar o resolvedor de conflitos personalizado (mesclagem)
description: Saiba como implementar um resolvedor de conflitos personalizado para uma publicação de mesclagem no SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8410ffdf38f8ae2d7dc5676debd13343c02c8f5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716827"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como implementar um resolvedor de conflitos personalizado para um artigo de mesclagem no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um [resolvedor personalizado com base em COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
 **Neste tópico**  
  
-   **Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Resolvedor baseado em COM](#COM)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode gravar seu próprio resolvedor de conflito personalizado como um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] em cada Publicador. Durante a sincronização, este procedimento armazenado é invocado quando são encontrados conflitos em um artigo no qual o resolvedor foi registrado. As informações sobre a linha de conflito são passadas pelo Agente de Mesclagem para os parâmetros necessários do procedimento. Resolvedores de conflito personalizados com base em procedimento armazenado sempre são criados no Publicador.  
  
> [!NOTE]  
>  Os resolvedores de procedimentos armazenados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são invocados apenas para resolver conflitos de linha baseados em alterações. Eles não podem ser usados para tratar outros tipos de conflitos como falhas de inserção acionadas por violações de PRIMARY KEY ou violações de restrições de índice exclusivo.
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>Para criar um resolvedor de conflitos personalizado com base em procedimentos armazenados  
  
1.  No Publicador em cada publicação ou banco de dados **msdb** , crie um novo procedimento armazenado de sistema que implementa os seguintes parâmetros requeridos:  
  
    |Parâmetro|Tipo de dados|DESCRIÇÃO|  
    |---------------|---------------|-----------------|  
    |**\@tableowner**|**sysname**|Nome do proprietário da tabela para a qual um conflito está estando resolvido. Esse é o proprietário para a tabela no banco de dados de publicação.|  
    |**\@tablename**|**sysname**|Nome da tabela para a qual um conflito está estando resolvido.|  
    |**\@rowguid**|**uniqueidentifier**|Identificador exclusivo da linha que tem o conflito.|  
    |**\@subscriber**|**sysname**|Nome do servidor do qual a alteração conflitante está sendo propagada.|  
    |**\@subscriber_db**|**sysname**|Nome do banco de dados do qual a alteração conflitante está sendo propagada.|  
    |**\@log_conflict OUTPUT**|**int**|Define se o processo de mesclagem deveria registrar o conflito para resolução posterior:<br /><br /> **0** = Não registre o conflito.<br /><br /> **1** = O Assinante é o perdedor de conflito.<br /><br /> **2** = O Publicador é o perdedor de conflito.|  
    |**\@conflict_message OUTPUT**|**nvarchar(512)**|Mensagem a ser dada sobre a resolução se o conflito for registrado.|  
    |**\@destowner**|**sysname**|O proprietário da tabela publicada no Assinante.|  
  
     Este procedimento armazenado usa os valores passados pelo Agente de Mesclagem para esses parâmetros para implementar a sua lógica de resolução de conflito personalizada. Ele deve retornar um conjunto de resultados de linha única que seja idêntico, em termos de estrutura, à tabela base e que contenha os valores de dados para a versão vencedora da linha.  
  
2.  Conceda permissões EXECUTE no procedimento armazenado para qualquer logon usado por Assinantes para conexão com o Publicador.  

#### <a name="use-a-custom-conflict-resolver-with-a-new-table-article"></a>Use um resolvedor de conflito personalizado com um novo artigo de tabela  
  
1. Execute [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir um artigo. 
1. Especifique um valor igual a **Resolvedor de Procedimentos Armazenados do** **Microsoft SQL Server** no parâmetro **\@article_resolver**. 
1. Especifique o nome do procedimento armazenado que implementa a lógica do resolvedor de conflitos para o parâmetro **\@resolver_info**. 

   Para saber mais, confira [Definir um artigo](../../relational-databases/replication/publish/define-an-article.md).
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Para usar um resolvedor de conflito personalizado com um artigo de tabela existente  
  
1.  Execute [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **\@publication**, **\@article**, um valor igual a **article_resolver** em **\@property** e um valor igual a **Resolvedor de Procedimentos Armazenados do** **Microsoft SQL Server** em **\@value**.  
  
2.  Execute [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **\@publication**, **\@article**, um valor de **resolver_info** para **\@property** e o nome do procedimento armazenado que implementa a lógica do resolvedor de conflitos para **\@value**.  
  
##  <a name="using-a-com-based-custom-resolver"></a><a name="COM"></a> Como usar um resolvedor personalizado com base em COM  
 O namespace <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> implementa uma interface que permite gravar lógicas empresariais complexas para tratar eventos e resolver conflitos que ocorram durante o processo de sincronização da replicação de Mesclagem. Para saber mais, confira como [implementar um manipulador de lógica de negócios em um artigo de Mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md). Você também pode gravar sua própria lógica corporativa personalizada com base em código nativo para resolver conflitos. Essa lógica é criada como um componente COM e compilada em bibliotecas de vínculo dinâmico (DLLs), usando produtos como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Esse tipo de resolvedor de conflitos personalizado com base em COM precisa implementar a interface **ICustomResolver**, que foi projetada especificamente para a resolução de conflitos.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>Para criar e registrar um resolvedor de conflitos personalizado com base em COM  
  
1.  Em um ambiente de criação compatível com o COM, adicione referências à biblioteca do Resolvedor de Conflitos Personalizado.  
  
2.  Para um projeto de Visual C++, use a diretiva #import para importar essa biblioteca para o seu projeto.  
  
3.  Crie uma classe que implemente a interface **ICustomResolver** .  
  
4.  Implemente certos métodos e propriedades.  
  
5.  Construa o projeto para criar o arquivo da biblioteca do resolvedor de conflitos.  
  
6.  Implemente a biblioteca no diretório que contém o executável do Agente de Mesclagem (normalmente \Microsoft SQL Server\100\COM).  
  
    > [!NOTE]  
    >  Um resolvedor de conflitos personalizado deve ser implantado no Assinante para uma assinatura pull, no Distribuidor para uma assinatura push ou no servidor Web usado com a sincronização da Web.  
  
7.  Registre a biblioteca do resolvedor de conflitos personalizado executando o regsvr32.exe no diretório de implantação, como segue:  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) para verificar se a biblioteca já não está registrada como um resolvedor de conflitos personalizado.  
  
9. Para registrar a biblioteca como um resolvedor de conflitos personalizado, execute [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) no Distributor. Especifique o nome amigável do objeto COM para **\@article_resolver**, a ID da biblioteca (CLSID) para **\@resolver_clsid** e um valor de **false** para **\@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Quando não for mais necessário, é possível cancelar o registro de um resolvedor de conflitos personalizado usando [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md).  
  
10. (Opcional) Em um cluster, repita as etapas de 6 a 9 para registrar o resolvedor personalizado em todos os nós do cluster. Essas etapas são necessárias para garantir que o resolvedor personalizado possa carregar adequadamente o reconciliador, depois de um failover.
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Para usar um resolvedor de conflito personalizado com um novo artigo de tabela  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome amigável do resolvedor desejado.  
  
2.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir um artigo. Especifique o nome amigável do resolvedor do artigo na etapa 1 para **\@article_resolver**. Para saber mais, confira [Definir um artigo](../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Para usar um resolvedor de conflito personalizado com um artigo de tabela existente  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome amigável do resolvedor desejado.  
  
2.  Execute [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **\@publication**, **\@article**, um valor de **article_resolver** para **\@property** e o nome amigável do resolvedor de artigo da etapa 1 para **\@value**.  
  

## <a name="see-also"></a>Confira também  
 [Detecção e resolução de conflito de replicação de Mesclagem Avançada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Resolvedores personalizados baseados em COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [Práticas recomendadas de segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
