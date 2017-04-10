---
title: "Implement a Custom Conflict Resolver for a Merge Article | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers"
  - "articles [SQL Server replication], conflict resolution"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Implement a Custom Conflict Resolver for a Merge Article
  Este tópico descreve como implementar o resolvedor de conflitos personalizado para um artigo de mesclagem em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um [resolvedor personalizado COM base em](../../relational-databases/replication/merge/com-based-custom-resolvers.md).  
  
 **Neste tópico**  
  
-   **Para implementar o resolvedor de conflitos personalizado para um artigo de mesclagem, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Resolvedor baseado em COM](#COM)  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Você pode gravar seu próprio resolvedor de conflito personalizado como um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] em cada Publicador. Durante a sincronização, esse procedimento armazenado será invocado quando forem encontrados conflitos em um artigo para o qual o resolvedor foi registrado, e a informação na linha em conflito é passada pelo Merge Agent para os parâmetros requeridos do procedimento. Resolvedores de conflito personalizados com base em procedimento armazenado sempre são criados no Publicador.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resolvedores de procedimento armazenado só sejam invocados para lidar com conflitos de linha baseados em alterações. Eles não podem ser usados para tratar de outros tipos de conflitos como falhas de inserção devido a violações de PRIMARY KEY ou violações de restrições de índice exclusivo.  
  
#### Para criar um resolvedor de conflitos personalizado com base em procedimentos armazenados  
  
1.  No Publicador em cada publicação ou banco de dados **msdb** , crie um novo procedimento armazenado de sistema que implementa os seguintes parâmetros requeridos:  
  
    |Parâmetro|Tipo de dados|Descrição|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|**sysname**|Nome do proprietário da tabela para a qual um conflito está estando resolvido. Esse é o proprietário para a tabela no banco de dados de publicação.|  
    |**@tablename**|**sysname**|Nome da tabela para a qual um conflito está estando resolvido.|  
    |**@rowguid**|**uniqueidentifier**|Identificador exclusivo para a linha que tem o conflito.|  
    |**@subscriber**|**sysname**|Nome do servidor de onde uma alteração conflitante está sendo propagada.|  
    |**@subscriber_db**|**sysname**|Nome do banco de dados de onde uma alteração conflitante está sendo propagada.|  
    |**@log_conflict OUTPUT**|**int**|Se o processo de mesclagem deveria registrar um conflito para resolução posterior:<br /><br /> **0** = Não registre o conflito.<br /><br /> **1** = assinante é o perdedor de conflito.<br /><br /> **2** = publicador é o perdedor de conflito.|  
    |**@conflict_message OUTPUT**|**nvarchar(512)**|Mensagem a ser dada sobre a resolução se o conflito for registrado.|  
    |**@destowner**|**sysname**|O proprietário da tabela publicada no Assinante.|  
  
     Esse procedimento armazenado usa os valores passados pelo Merge Agent para esses parâmetros para implementar sua lógica de resolução de conflito personalizada; ele deverá retornar um conjunto de resultados de linha única que é idêntico em estrutura à tabela base e contem os valores de dados para a versão vencedora da linha.  
  
2.  Conceda permissões EXECUTE no procedimento armazenado para qualquer logon usado por Assinantes para conexão com o Publicador.  
  
#### Para usar um resolvedor de conflito personalizado com um novo artigo de tabela  
  
1.  Executar [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir um artigo, especificando um valor de **Microsoft SQL** **resolvedor de procedimentos armazenados do servidor** para o **@article_resolver** parâmetro e o nome do procedimento armazenado que implementa a lógica do resolvedor de conflitos para o **@resolver_info** parâmetro. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para usar um resolvedor de conflito personalizado com um artigo de tabela existente  
  
1.  Executar [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, um valor de **article_resolver** para **@property**, e um valor de **Microsoft SQL** **Server armazenados ProcedureResolver** para **@value**.  
  
2.  Executar [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, um valor de **resolver_info** para **@property**, e o nome do procedimento armazenado que implementa a lógica do resolvedor de conflitos para **@value**.  
  
##  <a name="COM"></a> Usando um resolvedor personalizado com base em COM  
 O <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> namespace implementa uma interface que permite que você escreva a lógica comercial complexa para manipular eventos e resolver conflitos que ocorrem durante o processo de sincronização de replicação de mesclagem. Para obter mais informações, consulte [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md). Você também pode gravar sua própria lógica corporativa personalizada com base em código nativo para resolver conflitos. Essa lógica é criada como um componente COM e compilada em bibliotecas de vínculo dinâmico (DLL), usando produtos como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Um resolvedor de conflitos personalizado COM base em tal deve implementar o **ICustomResolver** interface, que foi desenvolvido especificamente para resolução de conflitos.  
  
#### Para criar e registrar um resolvedor de conflitos personalizado com base em COM  
  
1.  Em um ambiente de criação compatível com o COM, adicione referências à biblioteca do Resolvedor de Conflitos Personalizado.  
  
2.  Para um projeto de Visual C++, use a diretiva #import para importar essa biblioteca para o seu projeto.  
  
3.  Crie uma classe que implemente a interface **ICustomResolver** .  
  
4.  Implemente certos métodos e propriedades.  
  
5.  Construa o projeto para criar o arquivo da biblioteca do resolvedor de conflitos.  
  
6.  Implemente a biblioteca no diretório que contém o executável do agente de mesclagem (normalmente \Microsoft SQL Server\100\COM).  
  
    > [!NOTE]  
    >  Um resolvedor de conflitos personalizado deve ser implantado no Assinante para uma assinatura pull, no Distribuidor para uma assinatura push ou no servidor Web usado com a sincronização da Web.  
  
7.  Registre a biblioteca do resolvedor de conflitos personalizado usando o regsvr32.exe do diretório de implantação como segue:  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  No publicador, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) Para verificar que a biblioteca já não está registrada como um resolvedor de conflitos personalizado.  
  
9. Para registrar a biblioteca como um resolvedor de conflitos personalizado, execute [sp_registercustomresolver & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), no distribuidor. Especifique o nome amigável do objeto COM para **@article_resolver**, ID (CLSID da biblioteca) para **@resolver_clsid**, e um valor de **false** para **@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Quando forem mais necessárias, o resolvedor de conflitos personalizado pode ser cancelado usando [sp_unregistercustomresolver & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md).  
  
10. (Opcional) Em um cluster, repita as etapas de 5 a 8 para registrar o resolvedor personalizado em todos os nós do cluster. Isso é necessário para garantir que o resolvedor personalizado esteja apto a carregar adequadamente o reconciliador, seguindo um failover.  
  
#### Para usar um resolvedor de conflito personalizado com um novo artigo de tabela  
  
1.  No publicador, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e observe o nome amigável do resolvedor desejado.  
  
2.  No publicador do banco de dados de publicação, execute [sp_addmergearticle & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para definir um artigo. Especifique o nome amigável do resolvedor de artigo da etapa 1 para **@article_resolver**. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para usar um resolvedor de conflito personalizado com um artigo de tabela existente  
  
1.  No publicador, execute [sp_enumcustomresolvers & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e observe o nome amigável do resolvedor desejado.  
  
2.  Executar [sp_changemergearticle & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, um valor de **article_resolver** para **@property**, e o nome amigável do resolvedor de artigo da etapa 1 para **@value**.  
  
#### Exibindo um resolvedor personalizado de exemplo  
  
1.  Um exemplo está disponível nos arquivos de exemplo do SQL Server 2000. Baixe o **sql2000samples.cab** de [Exemplos atualizados do SQL Server 2000 Service Pack 3](http://www.microsoft.com/download/details.aspx?id=8560). Serão baixados 8 arquivos somando 6,9 MB.  
  
2.  Extraia os arquivos do arquivo .cab compactado que foi baixado.  
  
3.  Execute **setup.exe**  
  
    > [!NOTE]  
    >  Ao escolher as opções de instalação, é necessário apenas instalar os exemplos de **Replicação** . (O caminho de instalação padrão é **C:\Program arquivos (x86) \Microsoft SQL Server 2000 Samples\1033\\**)  
  
4.  Vá para a pasta de instalação. (A pasta padrão é **C:\Program arquivos (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  Execute o **unzip_sqlreplSP3.exe** programa.  
  
    > [!NOTE]  
    >  O resolvedor com de exemplo será instalado (por padrão) para o **C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** pasta.  
  
6.  No **subspres** pasta, localize todas as ocorrências de **#include sqlres.h** em todos os arquivos de origem e substituí-los com **#import "replrec" no_namespace, raw_interfaces_only**  
  
## Consulte também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Resolvedores personalizados com base em COM](../../relational-databases/replication/merge/com-based-custom-resolvers.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  