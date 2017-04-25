---
title: Anexar um banco de dados | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50e55a131e303a5303059a51797730f8bfab2581
ms.lasthandoff: 04/11/2017

---
# <a name="attach-a-database"></a>Anexar um banco de dados
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como anexar um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você pode usar este recurso para copiar, mover ou atualizar um banco de dados do SQL Server.  
  
 
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   O banco de dados primeiro deve ser desanexado. A tentativa de anexar um banco de dados que não foi desanexado retornará um erro. Para obter mais informações, veja [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md).  
  
-   Quando você anexa um banco de dados, todos os arquivos de dados (arquivos MDF e LDF) devem estar disponíveis. Se algum arquivo de dados tiver um caminho diferente de quando o banco de dados foi inicialmente criado ou anexado pela última vez, você deverá especificar o caminho atual do arquivo.  
  
-   Quando você anexar um banco de dados, se os arquivos MDF e LDF estiverem localizados em diretórios diferentes e um dos caminhos incluir \\\\?\GlobalRoot, a operação falhará.  
  
###  <a name="Recommendations"></a> Anexar é a melhor opção?  
 Recomendamos que você mova os bancos de dados utilizando o procedimento de realocação planejada ALTER DATABASE, em vez de utilizar desanexação e anexação, ao mover arquivos de banco de dados dentro da mesma instância. Para obter mais informações, veja [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md). 
 
Não recomendamos o uso de ações de desanexar e anexar para Backup e Recuperação. Não há backups de log de transações, e é possível excluir acidentalmente arquivos.
  
###  <a name="Security"></a> Segurança  
 As permissões de acesso ao arquivo são definidas durante algumas operações de banco de dados, inclusive desanexar ou anexar um banco de dados. Para obter informações sobre permissões de arquivo definidas sempre que um banco de dados é desanexado e anexado, veja [Protegendo dados e arquivos de log](http://technet.microsoft.com/library/ms189128.aspx) nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (ainda é uma leitura válida!) 
  
 Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados. Para saber mais sobre como anexar bancos de dados e informações sobre alterações que são feitas em metadados ao anexar um banco de dados, veja [Anexar e desanexar bancos de dados(SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão CREATE DATABASE, CREATE ANY DATABASE ou ALTER ANY DATABASE.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-attach-a-database"></a>Para anexar um banco de dados  
  
1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e clique para expandir a exibição dessa instância no SSMS.  
  
2.  Clique com o botão direito do mouse em **Bancos de dados** e clique em **Anexar**.  
  
3.  Na caixa de diálogo **Anexar Banco de Dados** , para especificar o banco de dados a ser anexado, clique em **Adicionar**. Na caixa de diálogo **Localizar Arquivos de Banco de Dados** , selecione a unidade de disco onde o banco de dados reside e expanda a árvore de diretório para localizar e selecionar o arquivo .mdf do banco de dados, por exemplo:  
  
     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    >  Tentar selecionar um banco de dados já anexado gera erro.  
  
     **Bancos de dados a serem anexados**  
     Exibe informações sobre os bancos de dados selecionados.  
  
     \<no column header>  
     Exibe um ícone que indica o status da operação de anexação. Os possíveis ícones são descritos em **Status** , abaixo).  
  
     **Local do Arquivo MDF**  
     Exibe o caminho e o nome de arquivo do arquivo MDF selecionado.  
  
     **Database Name**  
     Exibe o nome do banco de dados.  
  
     **Anexar como**  
     Opcionalmente, especifique um nome diferente para o banco de dados anexar como.  
  
     **Proprietário**  
     Fornece uma lista suspensa de possíveis proprietários de banco de dados dos quais você pode selecionar um proprietário diferente opcionalmente.  
  
     **Status**  
     Exibe o status do banco de dados de acordo com a seguinte tabela.  
  
    |Ícone|Texto de status|Descrição|  
    |----------|-----------------|-----------------|  
    |(No icon)|(Nenhum texto)|A operação de anexação não foi iniciada ou pode estar pendente para esse objeto. Esse é o padrão quando a caixa de diálogo é aberta.|  
    |Triângulo verde apontando para a direita|Em andamento|A operação de anexação foi iniciada mas não está completa.|  
    |Sinal de verificação verde|Success|O objeto foi anexado com êxito.|  
    |Círculo vermelho contendo uma cruz branca|Erro|A operação de anexação encontrou um erro e não foi concluída com êxito.|  
    |Círculo que contém dois quadrantes pretos (à esquerda e à direita) e dois quadrantes brancos (em cima e em baixo)|Stopped (parado)|A operação de anexação não foi completada com êxito porque o usuário interrompeu a operação.|  
    |Círculo que contém uma seta curvada que aponta para o sentido anti-horário|Revertida|A operação de anexação teve êxito, mas foi revertida devido a um erro ao se anexar outro objeto.|  
  
     **Mensagem**  
     Exibe uma mensagem em branco ou um hiperlink "Arquivo não encontrado"  
  
     **Adicionar**  
     Encontrar os arquivos de banco de dados principais necessários. Quando o usuário selecionar um arquivo .mdf , os respectivos campos são automaticamente preenchidos com informações aplicáveis da grade **Bancos de dados a serem anexados** .  
  
     **Remover**  
     Remove o arquivo selecionado da grade **Bancos de dados a serem anexados** .  
  
     **"** *<database_name>* **" detalhes do banco de dados**  
     Exibe os nomes dos arquivos a serem anexados. Para verificar ou alterar o nome do caminho de um arquivo, clique no botão **Procurar** (**…**).  
  
    > [!NOTE]  
    >  Se um arquivo não existir, a coluna **Mensagem** exibe "Não encontrado." Se um arquivo de log não for encontrado, ele existe em outro diretório ou foi excluído. Você precisa atualizar o caminho do arquivo na grade **detalhes do banco de dados** para indicar o local correto ou remover o arquivo de log da grade. Se um arquivo de dados .ndf não for encontrado, você precisará atualizar seu caminho na grade a fim de indicar o local correto.  
  
     **Nome do arquivo original**  
     Exibe o nome do arquivo anexado que pertence ao banco de dados.  
  
     **Tipo de arquivo**  
     Indica o tipo de arquivo, **Dados** ou **Log**.  
  
     **Caminho do arquivo atual**  
     Exibe o caminho para o arquivo de banco de dados selecionado. O caminho pode ser editado manualmente.  
  
     **Mensagem**  
     Exibe uma mensagem em branco ou um hiperlink “**Arquivo não encontrado**”.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-attach-a-database"></a>Para anexar um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Use a instrução [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) com a cláusula FOR ATTACH.  
  
     Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo anexa os arquivos do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e renomeia o banco de dados como `MyAdventureWorks`.  
  
    ```  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
  
    ```  
  
    > [!NOTE]  
    >  Se desejar, você poderá usar o procedimento armazenado [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) ou [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) . No entanto, esses procedimentos armazenados estendidos são removidos de uma versão futura do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aconselhamos usar CREATE DATABASE ... FOR ATTACH em vez disso.  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de atualizar um banco de dados do SQL Server  
 Após a atualização de um banco de dados usando o método anexar, o banco de dados se torna logo disponível e é atualizado automaticamente. Se o banco de dados tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados.  
  
 Se o nível de compatibilidade de um banco de dados de usuário for 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade for 90 ou inferior antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
  > [!NOTE]
  > Se você estiver conectando um banco de dados de uma instância que está executando o SQL Server 2014 ou anterior com o CDC (Change Data Capture) habilitado, você também precisará executar o comando abaixo para atualizar os metadados do CDC.
  ```
  USE <database name>
  EXEC sys.sp_cdc_vupgrade  
  ``` 
  
## <a name="see-also"></a>Consulte também  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md)  
  
  

