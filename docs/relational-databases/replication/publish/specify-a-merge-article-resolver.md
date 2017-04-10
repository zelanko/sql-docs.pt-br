---
title: "Especificar um resolvedor de artigo de mesclagem | Microsoft Docs"
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
  - "artigos [replicação do SQL Server], resolução de conflitos"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], resolvedores de artigo de mesclagem"
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Especificar um resolvedor de artigo de mesclagem
  Este tópico descreve como especificar um resolvedor de artigo de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar um resolvedor de artigo de mesclagem usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   A replicação de mesclagem permite os seguintes tipos de resolvedores de artigo:  
  
    -   O resolvedor padrão. O comportamento do resolvedor padrão depende se a assinatura é uma assinatura de cliente ou uma assinatura de servidor. Para obter mais informações sobre como especificar o tipo de assinatura, consulte [especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos e 40; SQL Server Management Studio e 41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md).  
  
    -   Você gravou um resolvedor personalizado, que pode ser um manipulador de lógica comercial (gravado em código gerenciado) ou um resolvedor personalizado baseado em COM. Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md). Se você precisar implementar uma lógica personalizada que é executada para cada linha replicada, não apenas para as linhas conflitantes, consulte [implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Um resolvedor padrão baseado em COM, que está incluído no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Para usar um resolvedor diferente do resolvedor padrão, você deve copiar o resolvedor ao computador em que é executado o Agente de Mesclagem e registrá-lo (se você estiver utilizando um manipulador de lógica comercial, ele deverá ser registrado também no Publicador). O Merge Agent é executado em:  
  
    -   O Distribuidor de uma assinatura push  
  
    -   O Assinante de uma assinatura pull  
  
    -   O servidor IIS (Serviços de informações da Internet) da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para uma assinatura pull que usa sincronização da Web  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Depois que o resolvedor estiver registrado, especificar que um artigo deve usar o resolvedor no **resolvedor** guia o **Propriedades do artigo - \< artigo>** caixa de diálogo, que está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar um resolvedor  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela.  
  
2.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
3.  Sobre o **Propriedades do artigo - \< artigo>** clique no **resolvedor** guia.  
  
4.  Selecione **usar um resolvedor personalizado (registrado no distribuidor)**, e, em seguida, na lista, clique no resolvedor.  
  
5.  Se o resolvedor requerer uma entrada (como um nome de coluna), especifique-na **Insira as informações necessárias para o resolvedor** caixa de texto.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Repita este processo para cada artigo que requer um resolvedor.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para registrar um resolvedor de conflitos personalizado  
  
1.  Se planejar registrar seu próprio resolvedor de conflitos personalizado, crie um dos tipos a seguir:  
  
    -   Resolvedor gerenciado baseado em códigos como um manipulador de lógica de negócios. Para obter mais informações, consulte [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Resolvedor baseado em procedimento armazenado e resolvedor baseado em COM. Para obter mais informações, consulte [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Para determinar se o resolvedor desejado já está registrado, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) no editor em qualquer banco de dados. Isso exibe uma descrição do resolvedor personalizado bem como do identificador de classe (CLSID) para cada resolvedor baseado em COM registrado no Distribuidor ou informações sobre o assembly gerenciado para cada manipulador de lógica de negócios registrado no Distribuidor.  
  
3.  Se o resolvedor personalizado desejado não estiver registrado, execute [sp_registercustomresolver & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) no distribuidor. Especifique um nome para o resolvedor de **@article_resolver**; para um manipulador de lógica de negócios, esse é o nome amigável do assembly. Para os resolvedores baseados em COM, especifique o CLSID do DLL para **@resolver_clsid**, e para um manipulador de lógica de negócios, especifique um valor de **true** para **@is_dotnet_assembly**, o nome do assembly de **@dotnet_assembly_name**, e o nome totalmente qualificado da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para **@dotnet_class_name**.  
  
    > [!NOTE]  
    >  Se um assembly de manipulador de lógica de negócios não está implantado no mesmo diretório do executável do Merge Agent, no mesmo diretório que o aplicativo que inicia sincronicamente o Merge Agent ou no cache de assembly global (GAC), você precisa especificar o caminho completo com o nome do assembly para **@dotnet_assembly_name**.  
  
4.  Se o resolvedor for um resolvedor baseado em COM:  
  
    -   Copiar o resolvedor personalizado DLL para o Distribuidor para assinaturas push ou para o Assinante para assinaturas pull.  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] resolvedores personalizados podem ser encontrados no [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]diretório COM.  
  
    -   Use o regsvr32.exe para registrar o resolvedor personalizado DLL no sistema operacional. Por exemplo, executando o seguinte no prompt de comando registra o Resolvedor de Conflitos Suplementar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Se o resolvedor for um manipulador de lógica de negócios, implante o assembly na mesma pasta do executável do Merge Agent (replmerg.exe), na mesma pasta do aplicativo que chama o Merge Agent ou na pasta especificada para o **@dotnet_assembly_name** parâmetro na etapa 3.  
  
    > [!NOTE]  
    >  O local de instalação padrão do executável Merge Agent é [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### Para especificar um resolvedor personalizado ao definir um artigo de mesclagem  
  
1.  Se você planeja usar um resolvedor de conflitos personalizado, crie e registre o resolvedor usando o procedimento acima.  
  
2.  No publicador, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome do resolvedor personalizado desejado no **valor** campo do conjunto de resultados.  
  
3.  No publicador do banco de dados de publicação, execute [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome do resolvedor da etapa 2 para **@article_resolver** e qualquer entrada necessária para o resolvedor personalizado usando o **@resolver_info** parâmetro. De resolvedores personalizados de baseados em procedimentos armazenados, **@resolver_info** é o nome do procedimento armazenado. Para obter mais informações sobre a entrada necessária para resolvedores fornecidos pela [!INCLUDE[msCoName](../../../includes/msconame-md.md)], consulte [Microsoft resolvedores COM base em](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md).  
  
#### Para especificar ou alterar um resolvedor personalizado para um artigo de mesclagem existente  
  
1.  Para determinar se um resolvedor personalizado foi definido para um artigo ou para obter o nome do resolvedor, execute [sp_helpmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Se houver um resolvedor personalizado definido para o artigo, seu nome será exibido no **article_resolver** campo. Nenhuma entrada fornecida ao resolvedor será exibida no **resolver_info** campo do conjunto de resultados.  
  
2.  No publicador, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e anote o nome do resolvedor personalizado desejado no **valor** campo do conjunto de resultados.  
  
3.  No publicador do banco de dados de publicação, execute [sp_changemergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **article_resolver**, incluindo o caminho completo para manipuladores de lógica de negócios para **@property**, e o nome do resolvedor personalizado desejado da etapa 2 para **@value**.  
  
4.  Para alterar qualquer entrada necessária para o resolvedor personalizado, execute [sp_changemergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) novamente. Especifique um valor de **resolver_info** para **@property** e qualquer entrada necessária para o resolvedor personalizado **@value**. De resolvedores personalizados de baseados em procedimentos armazenados, **@resolver_info** é o nome do procedimento armazenado. Para obter mais informações sobre a entrada necessária, consulte [Microsoft resolvedores COM base em](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md).  
  
#### Para cancelar o registro de um resolvedor de conflitos personalizado  
  
1.  No publicador, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e observe o nome do resolvedor personalizado para remover o **valor** campo do conjunto de resultados.  
  
2.  Executar [sp_unregistercustomresolver & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) no distribuidor. Especifique o nome completo do resolvedor personalizado da etapa 1 para **@article_resolver**.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo cria um novo artigo e especifica que o Resolvedor de Conflitos de Cálculo de Média [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser usado para calcular a média da coluna **UnitPrice** quando os conflitos ocorrerem.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 Esse exemplo altera um artigo a ser especificado usando o Resolvedor de Conflitos Suplementares [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para calcular a soma da coluna **UnitsOnOrder** quando os conflitos ocorrerem.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## Consulte também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  