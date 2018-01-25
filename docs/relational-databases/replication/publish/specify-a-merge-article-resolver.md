---
title: Especificar um resolvedor de artigo de mesclagem | Microsoft Docs
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
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: "39"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe9fd09314e8800921efbacec9289cf4e4df586b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="specify-a-merge-article-resolver"></a>Especificar um resolvedor de artigo de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como especificar um resolvedor de artigo de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar um resolvedor de artigo de mesclagem usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   A replicação de mesclagem permite os seguintes tipos de resolvedores de artigo:  
  
    -   O resolvedor padrão. O comportamento do resolvedor padrão depende se a assinatura é uma assinatura de cliente ou uma assinatura de servidor. Para obter mais informações sobre como especificar o tipo de assinatura, consulte [Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
    -   Você gravou um resolvedor personalizado, que pode ser um manipulador de lógica comercial (gravado em código gerenciado) ou um resolvedor personalizado baseado em COM. Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md). Se precisar implementar uma lógica personalizada que é executada para cada linha replicada, não apenas para as linhas conflitantes, consulte [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Um resolvedor padrão baseado em COM que é incluído com [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Para usar um resolvedor diferente do resolvedor padrão, você deve copiar o resolvedor ao computador em que é executado o Agente de Mesclagem e registrá-lo (se você estiver utilizando um manipulador de lógica comercial, ele deverá ser registrado também no Publicador). O Merge Agent é executado em:  
  
    -   O Distribuidor de uma assinatura push  
  
    -   O Assinante de uma assinatura pull  
  
    -   O servidor IIS (Serviços de informações da Internet) da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para uma assinatura pull que usa sincronização da Web  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Depois que o resolvedor estiver registrado, especifique se um artigo deverá usar o resolvedor na guia **Resolvedor** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**, disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades de Publicação –\<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-resolver"></a>Para especificar um resolvedor  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione uma tabela.  
  
2.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
3.  Na página **Propriedades do Artigo – \<Artigo>**, clique na guia **Resolvedor**.  
  
4.  Selecione **Usar um resolvedor personalizado (registrado no Distribuidor)**e então na lista, clique no resolvedor.  
  
5.  Se o resolvedor requerer uma entrada (por exemplo, um nome de coluna), especifique-a na caixa de texto **Insira as informações necessárias para o resolvedor** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Repita este processo para cada artigo que requer um resolvedor.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>Para registrar um resolvedor de conflitos personalizado  
  
1.  Se planejar registrar seu próprio resolvedor de conflitos personalizado, crie um dos tipos a seguir:  
  
    -   Resolvedor gerenciado baseado em códigos como um manipulador de lógica de negócios. Para obter mais informações, consulte [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Resolvedor baseado em procedimento armazenado e resolvedor baseado em COM. Para obter mais informações, consulte [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Para determinar se o resolvedor desejado já está registrado, execute o [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) no Publicador em qualquer banco de dados. Isso exibe uma descrição do resolvedor personalizado bem como do identificador de classe (CLSID) para cada resolvedor baseado em COM registrado no Distribuidor ou informações sobre o assembly gerenciado para cada manipulador de lógica de negócios registrado no Distribuidor.  
  
3.  Se o resolvedor personalizado desejado ainda não está registrado, execute o [sp_registercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) no Distribuidor. Especifique um nome para o resolvedor para **@article_resolver**; para um manipulador de lógica de negócios, este é o nome amigável para o assembly. Para os resolvedores baseados em COM, especifique o CLSID do DLL para **@resolver_clsid**e para um manipulador de lógica de negócios, especifique um valor **true** para **@is_dotnet_assembly**, o nome do assembly para **@dotnet_assembly_name**e o nome totalmente qualificado da classe que substitui o <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Se um assembly de manipuladores de lógica de negócios não estiver implantado no mesmo diretório que o executável Merge Agent, no mesmo diretório que o aplicativo que inicia de maneira síncrona o Merge Agent ou no GAC (cache de assembly global), você deverá especificar o caminho completo com o nome do assembly para **@dotnet_assembly_name**.  
  
4.  Se o resolvedor for um resolvedor baseado em COM:  
  
    -   Copiar o resolvedor personalizado DLL para o Distribuidor para assinaturas push ou para o Assinante para assinaturas pull.  
  
        > [!NOTE]  
        >  Resolvedores personalizados[!INCLUDE[msCoName](../../../includes/msconame-md.md)] podem ser localizados no diretório [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
    -   Use o regsvr32.exe para registrar o resolvedor personalizado DLL no sistema operacional. Por exemplo, executando o seguinte no prompt de comando registra o Resolvedor de Conflitos Suplementar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Se o resolvedor for um manipulador de lógica de negócios, implemente o assembly na mesma pasta do executável Merge Agent, (replmerg.exe), na mesma pasta do aplicativo que chama o Merge Agent ou na pasta especificada para o parâmetro **@dotnet_assembly_name** na etapa 3.  
  
    > [!NOTE]  
    >  O local de instalação padrão do executável Merge Agent é [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>Para especificar um resolvedor personalizado ao definir um artigo de mesclagem  
  
1.  Se você planeja usar um resolvedor de conflitos personalizado, crie e registre o resolvedor usando o procedimento acima.  
  
2.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome do resolvedor personalizado desejado no campo **valor** do conjunto de resultados.  
  
3.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome do resolvedor da etapa 2 para **@article_resolver** e qualquer entrada necessária para o resolvedor personalizado usando o parâmetro **@resolver_info** . Para os resolvedores personalizados baseados em procedimentos armazenados, o **@resolver_info** é o nome do procedimento armazenado. Para obter mais informações sobre a entrada necessária para os resolvedores fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)], consulte [Resolvedores baseados em COM da Microsoft](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>Para especificar ou alterar um resolvedor personalizado para um artigo de mesclagem existente  
  
1.  Para determinar se um resolvedor personalizado foi definido para um artigo ou para obter o nome do resolvedor, execute [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Se houver um resolvedor personalizado definido para o artigo, seu nome será exibido no campo **article_resolver** . Qualquer entrada fornecida ao resolvedor será exibida no campo **resolver_info** do conjunto de resultados.  
  
2.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome do resolvedor personalizado desejado no campo **valor** do conjunto de resultados.  
  
3.  No Publicador no banco de dados de publicação, execute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **article_resolver**, inclusive o caminho completo para os manipuladores de lógica de negócios, para **@property**e o nome do resolvedor personalizado desejado da etapa 2 para **@value**.  
  
4.  Para alterar qualquer entrada necessária para o resolvedor personalizado, execute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) novamente. Especifique um valor de **resolver_info** para **@property** e qualquer entrada necessária para o resolvedor personalizado para **@value**. Para os resolvedores personalizados baseados em procedimentos armazenados, o **@resolver_info** é o nome do procedimento armazenado. Para obter mais informações sobre as entradas requeridas, consulte [Resolvedores baseados em COM da Microsoft](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>Para cancelar o registro de um resolvedor de conflitos personalizado  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome do resolvedor personalizado a ser removido no campo **valor** do conjunto de resultados.  
  
2.  Execute [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) no Distribuidor. Especifique o nome completo do resolvedor personalizado da etapa 1 para **@article_resolver**.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo cria um novo artigo e especifica que o Resolvedor de Conflitos de Cálculo de Média [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser usado para calcular a média da coluna **UnitPrice** quando os conflitos ocorrerem.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 Esse exemplo altera um artigo a ser especificado usando o Resolvedor de Conflitos Suplementares [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para calcular a soma da coluna **UnitsOnOrder** quando os conflitos ocorrerem.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
