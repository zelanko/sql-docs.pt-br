---
title: Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 47d0f7c4eb6c78b9e551fafdc1e018a27604086e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721233"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>Implementar o resolvedor de conflitos personalizado para um artigo de mesclagem
  Este tópico descreve como implementar o resolvedor de conflitos personalizado para um artigo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de mesclagem no usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um [resolvedor personalizado baseado em com](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
 **Neste tópico**  
  
-   **Para implementar o resolvedor de conflitos personalizado para um artigo de mesclagem, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Resolvedor baseado em COM](#COM)  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode gravar seu próprio resolvedor de conflito personalizado como um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] em cada Publicador. Durante a sincronização, esse procedimento armazenado será invocado quando forem encontrados conflitos em um artigo para o qual o resolvedor foi registrado, e a informação na linha em conflito é passada pelo Merge Agent para os parâmetros requeridos do procedimento. Resolvedores de conflito personalizados com base em procedimento armazenado sempre são criados no Publicador.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os resolvedores de procedimento armazenado são invocados apenas para lidar com conflitos baseados em alteração de linha. Eles não podem ser usados para tratar de outros tipos de conflitos como falhas de inserção devido a violações de PRIMARY KEY ou violações de restrições de índice exclusivo.  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>Para criar um resolvedor de conflitos personalizado com base em procedimentos armazenados  
  
1.  No Publicador em cada publicação ou banco de dados **msdb** , crie um novo procedimento armazenado de sistema que implementa os seguintes parâmetros requeridos:  
  
    |Parâmetro|Tipo de dados|DESCRIÇÃO|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|Nome do proprietário da tabela para a qual um conflito está estando resolvido. Esse é o proprietário para a tabela no banco de dados de publicação.|  
    |**@tablename**|`sysname`|Nome da tabela para a qual um conflito está estando resolvido.|  
    |**@rowguid**|`uniqueidentifier`|Identificador exclusivo para a linha que tem o conflito.|  
    |**@subscriber**|`sysname`|Nome do servidor de onde uma alteração conflitante está sendo propagada.|  
    |**@subscriber_db**|`sysname`|Nome do banco de dados de onde uma alteração conflitante está sendo propagada.|  
    |**@log_conflictDER**|`int`|Se o processo de mesclagem deveria registrar um conflito para resolução posterior:<br /><br /> **0** = Não registre o conflito.<br /><br /> **1** = O Assinante é o perdedor de conflito.<br /><br /> **2** = O Publicador é o perdedor de conflito.|  
    |**@conflict_messageDER**|`nvarchar(512)`|Mensagem a ser dada sobre a resolução se o conflito for registrado.|  
    |**@destowner**|`sysname`|O proprietário da tabela publicada no Assinante.|  
  
     Esse procedimento armazenado usa os valores passados pelo Merge Agent para esses parâmetros para implementar sua lógica de resolução de conflito personalizada; ele deverá retornar um conjunto de resultados de linha única que é idêntico em estrutura à tabela base e contem os valores de dados para a versão vencedora da linha.  
  
2.  Conceda permissões EXECUTE no procedimento armazenado para qualquer logon usado por Assinantes para conexão com o Publicador.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Para usar um resolvedor de conflito personalizado com um novo artigo de tabela  
  
1.  Execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir um artigo, especificando o valor de **Resolvedor de Procedimentos Armazenados do** **MicrosoftSQL** para o parâmetro **@article_resolver** e o nome do procedimento armazenado que implementa a lógica do resolvedor de conflitos para o parâmetro **@resolver_info**. Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Para usar um resolvedor de conflito personalizado com um artigo de tabela existente  
  
1.  Execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, um valor de **article_resolver** para **@property**, e um valor de servidor **MicrosoftSQL** **armazenado ProcedureResolver** para **@value**.  
  
2.  Execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, um valor de **resolver_info** para **@property**, e o nome do procedimento armazenado que implementa a lógica do resolvedor de **@value**conflitos para.  
  
##  <a name="COM"></a>Usando um resolvedor personalizado com base em COM  
 O namespace <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> implementa uma interface, permitindo que você grave lógicas empresariais complexas para manipular eventos e resolva conflitos que ocorram durante o processo de sincronização da replicação de mesclagem. Para obter mais informações, consulte [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](implement-a-business-logic-handler-for-a-merge-article.md). Você também pode gravar sua própria lógica corporativa personalizada com base em código nativo para resolver conflitos. Essa lógica é criada como um componente COM e compilada em bibliotecas de vínculo dinâmico (DLL), usando produtos como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Um resolvedor de conflitos personalizado baseado em COM deve implementar a interface **ICustomResolver** , que é projetada especificamente para resolução de conflitos.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>Para criar e registrar um resolvedor de conflitos personalizado com base em COM  
  
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
  
8.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) para verificar se a biblioteca já não está registrada como um resolvedor de conflitos personalizado.  
  
9. Para registrar a biblioteca como um resolvedor de conflitos personalizado, execute [sp_registercustomresolver &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql), no distribuidor. Especifique o nome amigável do **@article_resolver**objeto com para, a ID da biblioteca (CLSID) para **@resolver_clsid**e um valor de `false` para. **@is_dotnet_assembly**  
  
    > [!NOTE]  
    >  Quando não for mais necessário, um resolvedor de conflitos personalizado poderá ter o registrado cancelado, usando [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql).  
  
10. (Opcional) Em um cluster, repita as etapas de 5 a 8 para registrar o resolvedor personalizado em todos os nós do cluster. Isso é necessário para garantir que o resolvedor personalizado esteja apto a carregar adequadamente o reconciliador, seguindo um failover.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Para usar um resolvedor de conflito personalizado com um novo artigo de tabela  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e anote o nome amigável do resolvedor desejado.  
  
2.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir um artigo. Especifique o nome amigável do resolvedor de artigo da etapa 1 **@article_resolver**para. Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Para usar um resolvedor de conflito personalizado com um artigo de tabela existente  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e anote o nome amigável do resolvedor desejado.  
  
2.  Execute [sp_changemergearticle &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, um valor de **article_resolver** para **@property**e o nome amigável do resolvedor de artigo da etapa 1 para **@value**.  
  
#### <a name="viewing-a-sample-custom-resolver"></a>Exibindo um resolvedor personalizado de exemplo  
  
1.  Um exemplo está disponível nos arquivos de exemplo do SQL Server 2000. Baixe o [**sql2000samples. zip**](https://github.com/Microsoft/sql-server-samples/blob/master/samples/tutorials/Miscellaneous/sql2000samples.zip). Isso baixa 3 arquivos de valor para 6,9 MB.  
  
2.  Extraia os arquivos do arquivo .cab compactado que foi baixado.  
  
3.  Executar **Setup. exe**  
  
    > [!NOTE]  
    >  Ao escolher as opções de instalação, é necessário apenas instalar os exemplos de **Replicação** . (O caminho de instalação padrão é **C:\Program Files (x86) \microsoft SQL Server\\2000 Samples\1033**)  
  
4.  Vá para a pasta de instalação. (A pasta padrão é **C:\Arquivos de Programas (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  Execute o programa **unzip_sqlreplSP3.exe** .  
  
    > [!NOTE]  
    >  O resolvedor com de exemplo será instalado (por padrão) para a pasta **C:\Arquivos de Programas (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** .  
  
6.  Na pasta **subspres** , localize todas as ocorrências de **#include sqlres.h** em todos os arquivos de origem e substitua-os por **#import "replrec.dll" no_namespace, raw_interfaces_only**  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Resolvedores personalizados baseados em COM](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
