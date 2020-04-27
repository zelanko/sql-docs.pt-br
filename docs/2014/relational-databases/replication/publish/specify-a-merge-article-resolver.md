---
title: Especificar um resolvedor de artigo de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 388d400160e3fa7b3240c7a9c014bcf36ae25f3a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68212090"
---
# <a name="specify-a-merge-article-resolver"></a>Especificar um resolvedor de artigo de mesclagem
  Este tópico descreve como especificar um resolvedor de artigo de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar um resolvedor de artigo de mesclagem usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   A replicação de mesclagem permite os seguintes tipos de resolvedores de artigo:  
  
    -   O resolvedor padrão. O comportamento do resolvedor padrão depende se a assinatura é uma assinatura de cliente ou uma assinatura de servidor. Para obter mais informações sobre como especificar o tipo de assinatura, consulte [Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos &#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
    -   Você gravou um resolvedor personalizado, que pode ser um manipulador de lógica comercial (gravado em código gerenciado) ou um resolvedor personalizado baseado em COM. Para obter mais informações, consulte [detecção e resolução de conflitos de replicação de mesclagem avançada](../merge/advanced-merge-replication-conflict-detection-and-resolution.md). Se precisar implementar uma lógica personalizada que é executada para cada linha replicada, não apenas para as linhas conflitantes, consulte [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Um resolvedor padrão baseado em COM, que está incluído [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]no.  
  
-   Para usar um resolvedor diferente do resolvedor padrão, você deve copiar o resolvedor ao computador em que é executado o Agente de Mesclagem e registrá-lo (se você estiver utilizando um manipulador de lógica comercial, ele deverá ser registrado também no Publicador). O Merge Agent é executado em:  
  
    -   O Distribuidor de uma assinatura push  
  
    -   O Assinante de uma assinatura pull  
  
    -   O servidor IIS (Serviços de informações da Internet) da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para uma assinatura pull que usa sincronização da Web  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Depois que o resolvedor estiver registrado, especifique se um artigo deverá usar o resolvedor na guia **Resolvedor** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**, disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades de Publicação –\<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-resolver"></a>Para especificar um resolvedor  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione uma tabela.  
  
2.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
3.  Na página **Propriedades do Artigo – \<Artigo>**, clique na guia **Resolvedor**.  
  
4.  Selecione **Usar um resolvedor personalizado (registrado no Distribuidor)** e então na lista, clique no resolvedor.  
  
5.  Se o resolvedor requerer uma entrada (por exemplo, um nome de coluna), especifique-a na caixa de texto **Insira as informações necessárias para o resolvedor** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Repita este processo para cada artigo que requer um resolvedor.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>Para registrar um resolvedor de conflitos personalizado  
  
1.  Se planejar registrar seu próprio resolvedor de conflitos personalizado, crie um dos tipos a seguir:  
  
    -   Resolvedor gerenciado baseado em códigos como um manipulador de lógica de negócios. Para obter mais informações, consulte [implementar um manipulador de lógica de negócios para um artigo de mesclagem](../implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Resolvedor baseado em procedimento armazenado e resolvedor baseado em COM. Para obter mais informações, consulte [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](../implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Para determinar se o resolvedor desejado já está registrado, execute o [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) no Publicador em qualquer banco de dados. Isso exibe uma descrição do resolvedor personalizado bem como do identificador de classe (CLSID) para cada resolvedor baseado em COM registrado no Distribuidor ou informações sobre o assembly gerenciado para cada manipulador de lógica de negócios registrado no Distribuidor.  
  
3.  Se o resolvedor personalizado desejado ainda não está registrado, execute o [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql) no Distribuidor. Especifique um nome para o resolvedor **@article_resolver**para; para um manipulador de lógica de negócios, esse é o nome amigável do assembly. Para resolvedores baseados em COM, especifique **@resolver_clsid**o CLSID da dll para, e para um manipulador de lógica de negócios, especifique um valor de `true` para **@is_dotnet_assembly**, o nome do assembly para **@dotnet_assembly_name**e o nome totalmente qualificado da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para. **@dotnet_class_name**  
  
    > [!NOTE]  
    >  Se um assembly de manipulador de lógica de negócios não estiver implantado no mesmo diretório que o Agente de Mesclagem executável, no mesmo diretório que o aplicativo que inicia de forma síncrona o Agente de Mesclagem ou no GAC (cache de assembly global), você precisará especificar o caminho completo com **@dotnet_assembly_name**o nome do assembly para.  
  
4.  Se o resolvedor for um resolvedor baseado em COM:  
  
    -   Copiar o resolvedor personalizado DLL para o Distribuidor para assinaturas push ou para o Assinante para assinaturas pull.  
  
        > [!NOTE]  
        >  Resolvedores personalizados[!INCLUDE[msCoName](../../../includes/msconame-md.md)] podem ser localizados no diretório [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
    -   Use o regsvr32.exe para registrar o resolvedor personalizado DLL no sistema operacional. Por exemplo, executando o seguinte no prompt de comando registra o Resolvedor de Conflitos Suplementar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Se o resolvedor for um manipulador de lógica de negócios, implante o assembly na mesma pasta que o Agente de Mesclagem executável (replmerg. exe), na mesma pasta que um aplicativo que invoca o Agente de Mesclagem ou na pasta especificada para o **@dotnet_assembly_name** parâmetro na etapa 3.  
  
    > [!NOTE]  
    >  O local de instalação padrão do executável Merge Agent é [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>Para especificar um resolvedor personalizado ao definir um artigo de mesclagem  
  
1.  Se você planeja usar um resolvedor de conflitos personalizado, crie e registre o resolvedor usando o procedimento acima.  
  
2.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e anote o nome do resolvedor personalizado desejado no campo **valor** do conjunto de resultados.  
  
3.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique o nome do resolvedor da etapa 2 para **@article_resolver** e qualquer entrada necessária para o resolvedor personalizado usando **@resolver_info** o parâmetro. Para resolvedores personalizados baseados em procedimentos armazenados, **@resolver_info** é o nome do procedimento armazenado. Para obter mais informações sobre a entrada necessária para os resolvedores fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)], consulte [Resolvedores baseados em COM da Microsoft](../merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>Para especificar ou alterar um resolvedor personalizado para um artigo de mesclagem existente  
  
1.  Para determinar se um resolvedor personalizado foi definido para um artigo ou para obter o nome do resolvedor, execute [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Se houver um resolvedor personalizado definido para o artigo, seu nome será exibido no campo **article_resolver** . Qualquer entrada fornecida ao resolvedor será exibida no campo **resolver_info** do conjunto de resultados.  
  
2.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e anote o nome do resolvedor personalizado desejado no campo **valor** do conjunto de resultados.  
  
3.  No Publicador no banco de dados de publicação, execute [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **article_resolver**, inclusive o caminho completo para os manipuladores de lógica de negócios, para **@property**e o nome do resolvedor personalizado desejado da etapa 2 para **@value**.  
  
4.  Para alterar qualquer entrada necessária para o resolvedor personalizado, execute [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) novamente. Especifique um valor de **resolver_info** para **@property** e qualquer entrada necessária para o resolvedor personalizado para **@value**. Para resolvedores personalizados baseados em procedimentos armazenados, **@resolver_info** é o nome do procedimento armazenado. Para obter mais informações sobre as entradas requeridas, consulte [Resolvedores baseados em COM da Microsoft](../merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>Para cancelar o registro de um resolvedor de conflitos personalizado  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e anote o nome do resolvedor personalizado a ser removido no campo **valor** do conjunto de resultados.  
  
2.  Execute [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql) no Distribuidor. Especifique o nome completo do resolvedor personalizado da etapa 1 para **@article_resolver**.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a>Exemplos (Transact-SQL)  
 Esse exemplo cria um novo artigo e especifica que o Resolvedor de Conflitos de Cálculo de Média [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser usado para calcular a média da coluna **UnitPrice** quando os conflitos ocorrerem.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_addmerge_resolver)]  
  
 Esse exemplo altera um artigo a ser especificado usando o Resolvedor de Conflitos Suplementares [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para calcular a soma da coluna **UnitsOnOrder** quando os conflitos ocorrerem.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_changemerge_resolver)]  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflitos de replicação de mesclagem avançada](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
