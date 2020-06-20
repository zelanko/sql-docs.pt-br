---
title: Suporte ao SQL Server Management Studio para OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ee847b5f-6a1a-448e-a746-d61a023881ff
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 644ba0cfdbe2f0043364c633676bbc536c641efa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025792"
---
# <a name="sql-server-management-studio-support-for-in-memory-oltp"></a>Suporte ao SQL Server Management Studio para OLTP na memória
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é um ambiente integrado para gerenciar a infraestrutura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece ferramentas para configurar, monitorar e administrar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md).  
  
 As tarefas neste tópico descrevem como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar tabelas com otimização de memória, índices em tabelas com otimização de memória, procedimentos armazenados nativamente compilados e tipos de tabela com otimização de memória definidos pelo usuário.  
  
 Para obter informações sobre como criar tabelas com otimização de memória de forma programática, veja [Criando uma tabela com otimização de memória e um procedimento armazenado compilado de modo nativo](creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
### <a name="to-create-a-database-with-a-memory-optimized-data-filegroup"></a>Para criar um banco de dados com um grupo de arquivos de dados com otimização de memória.  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e expanda-a.  
  
2.  Clique com o botão direito do mouse em **Bancos de Dados**e clique em **Novo Banco de Dados**.  
  
3.  Para adicionar um novo grupo de arquivos de dados com otimização de memória, clique na página **Grupos de Arquivos** . Em **MEMORY OPTIMIZED DATA**, clique em **Adicionar grupo de arquivos** e insira o nome do grupo de arquivos de dados com otimização de memória.  A coluna rotulada **Arquivos FILESTREAM** representa o número de contêineres no grupo de arquivos. Os contêineres são adicionados na página **Geral** .  
  
4.  Para adicionar um arquivo (contêiner) ao grupo de arquivos, clique na página **Geral** . Em **Arquivos de Banco de Dados**, clique em **Adicionar**. Selecione **Tipo de Arquivo** como **Dados de FILESTREAM**, especifique o nome lógico do contêiner, selecione o grupo de arquivos com otimização de memória e verifique se **Expansão Automática/Tamanho Máximo** está definido como **Ilimitado**.  
  
     Para obter mais informações sobre como criar um novo banco de dados usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], veja [Criar um banco de dados](../databases/create-a-database.md).  
  
### <a name="to-create-a-memory-optimized-table"></a>Para criar uma tabela com otimização de memória  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse no nó **Tabelas** do banco de dados, clique em **Novo**e clique em **Tabela com Otimização de Memória**.  
  
     É exibido um modelo para criar tabelas com otimização de memória.  
  
2.  Para substituir os parâmetros de modelo, clique em **Especificar Valores para Parâmetros de Modelo** no menu **Consulta** .  
  
     Para obter mais informações sobre como usar modelos, veja [Explorador de Modelos](../../ssms/template/template-explorer.md).  
  
3.  No **Pesquisador de Objetos**, as tabelas serão ordenadas primeiro por tabelas com base em disco seguidas por tabelas com otimização de memória. Use os **Detalhes do Pesquisador de Objetos** para ver todas as tabelas ordenadas por nome.  
  
### <a name="to-create-a-natively-compiled-stored-procedure"></a>Para criar um procedimento armazenado compilado nativamente  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse no nó **Procedimentos Armazenados** do banco de dados, clique em **Novo**e clique em **Procedimento Armazenado Compilado de Modo Nativo**.  
  
     É exibido um modelo para criar procedimentos armazenados compilados nativamente.  
  
2.  Para substituir os parâmetros de modelo, clique em **Especificar Valores para Parâmetros de Modelo** no **menu Consulta**.  
  
     Para obter mais informações sobre como criar e usar um novo procedimento armazenado, veja [Criar um procedimento armazenado](../stored-procedures/create-a-stored-procedure.md).  
  
### <a name="to-create-a-user-defined-memory-optimized-table-type"></a>Para criar um tipo de tabela com otimização de memória definido pelo usuário  
  
1.  Em **Pesquisador de Objetos**, expanda o nó **Tipos** do seu banco de dados, clique com o botão direito do mouse no nó **Tipos de Tabela Definidos pelo Usuário** , clique em **Novo**e em **Tipo de Tabela com Otimização de Memória Definido pelo Usuário**.  
  
     É exibido um modelo para a criação do tipo de tabela com otimização de memória definido pelo usuário.  
  
2.  Para substituir os parâmetros de modelo, clique em **Especificar Valores para Parâmetros de Modelo** no menu **Consulta** .  
  
     Para obter mais informações sobre como criar e usar um novo procedimento armazenado, veja [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql).  
  
## <a name="memory-monitoring"></a>Monitoramento da memória  
  
#### <a name="view-memory-usage-by-memory-optimized-objects-report"></a>Exibir uso da memória por relatório de objetos com otimização de memória  
  
-   No **Pesquisador de Objetos**, clique com o botão direito do mouse no banco de dados, clique em **Relatórios**, clique em **Relatórios Padrão**e clique em **Uso de Memória por Objetos com Otimização de Memória**.  
  
     Esse relatório fornece dados detalhados sobre a utilização do espaço da memória pelos objetos com otimização de memória no banco de dados.  
  
#### <a name="view-properties-for-allocated-and-used-memory-for-a-table-database"></a>Exibir propriedades da memória alocada e usada para uma tabela, um banco de dados  
  
1.  Para obter informações sobre o uso na memória:  
  
    -   No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com otimização de memória, clique em **Propriedades**e na página **Armazenamento** . O valor da propriedade **Espaço de Dados** indica a memória usada pelos dados na tabela. O valor da propriedade **Espaço do Índice** indica a memória usada pelos índices na tabela.  
  
    -   No **Pesquisador de Objetos**, clique com o botão direito do mouse no banco de dados, clique em **Propriedades**e clique na página **Geral** . O valor da propriedade **Memória Alocada a Objetos com Otimização de Memória** indica a memória alocada a objetos com otimização de memória no banco de dados. O valor da propriedade **Memória Usada por Objetos com Otimização de Memória** indica a memória usada por objetos com otimização de memória no banco de dados.  
  
## <a name="supported-features-in-ssmanstudiofull"></a>Recursos com suporte no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dá suporte a recursos e operações que têm suporte no mecanismo de banco de dados em bancos de dados com grupo de arquivos de dados com otimização de memória, tabelas com otimização de memória, índices e procedimentos armazenados compilados de modo nativo.  
  
 No banco de dados, na tabela, no procedimento armazenado, no tipo de tabela definido pelo usuário ou nos objetos de índice, os seguintes recursos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] foram atualizados ou estendidos para oferecer suporte à OLTP na memória.  
  
-   Pesquisador de Objetos  
  
    -   Menus de contexto  
  
    -   Configurações de filtro  
  
    -   Gerar Script como  
  
    -   Tarefas  
  
    -   Relatórios  
  
    -   Propriedades  
  
    -   Tarefas do banco de dados:  
  
        -   Anexar e desanexar um banco de dados que contém tabelas com otimização de memória.  
  
             A interface do usuário **Anexar Bancos de Dados** não exibe o grupo de arquivos de dados com otimização de memória. Porém, você pode continuar anexando o banco de dados e ele será anexado corretamente.  
  
            > [!NOTE]  
            >  Se você quiser usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para anexar um banco de dados que tem um contêiner de grupo de arquivos de dados com otimização de memória, e se esse contêiner tiver sido criado em outro computador, o local do contêiner de grupo de arquivos de dados com otimização de memória deverá ser o mesmo em ambos os computadores. Se você quiser que o local do contêiner de grupo de arquivos de dados com otimização de memória do banco de dados seja diferente no novo computador, poderá usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para anexar o banco de dados. No exemplo a seguir, o local do contêiner de grupo de arquivos de dados com otimização de memória no novo computador é C:\Folder2. Mas, quando o contêiner de grupo de arquivos de dados com otimização de memória foi criado, no primeiro computador, o local era C:\Folder1.  
            >   
            >  `CREATE DATABASE[imoltp] ON`  
            >   
            >  `(NAME =N'imoltp',FILENAME=N'C:\Folder2\imoltp.mdf'),`  
            >   
            >  `(NAME =N'imoltp_mod1',FILENAME=N'C:\Folder2\imoltp_mod1'),`  
            >   
            >  `(NAME =N'imoltp_log',FILENAME=N'C:\Folder2\imoltp_log.ldf')`  
            >   
            >  `FOR ATTACH`  
            >   
            >  `GO`  
  
        -   Gere scripts.  
  
             No **Assistente para Gerar e Publicar Scripts**, o valor padrão para a opção de script **Verificar a existência do objeto** é FALSE. Se o valor da opção de script **Verificar a existência do objeto** estiver definido como TRUE na tela **Definir Opções de Script** do assistente, o script gerado conterá “CREATE PROCEDURE <procedure_name> AS” e “ALTER PROCEDURE <procedure_name> <procedure_definition>”. Quando executado, o script gerado retornará um erro pois ALTER PROCEDURE não tem suporte em procedimentos armazenados compilados de modo nativo.  
  
             Para alterar o script gerado para cada procedimento armazenado compilado de modo nativo:  
  
            1.  Em "CREATE PROCEDURE <nome_do_procedimento> AS", substitua "AS" por "<definição_do_procedimento>".  
  
            2.  Exclua "ALTER PROCEDURE <nome_do_procedimento> <definição_do_procedimento>".  
  
        -   Copie bancos de dados. Para bancos de dados que têm objetos com otimização de memória, a criação do banco de dados no servidor de destino e a transferência de dados não serão executadas em uma transação.  
  
        -   Importe e exporte dados. Use a opção **Copiar dados de uma ou mais tabelas ou exibições do Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** . Se a tabela de destino for uma tabela com otimização de memória que não existe no banco de dados de destino:  
  
            1.  No **Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** , na tela **Especificar Cópia ou Consulta de Tabela**, selecione **Copiar dados de uma ou mais tabelas ou exibições**. Em seguida, clique em **Próximo**.  
  
            2.  Clique em **Editar Mapeamentos**. Selecione **Criar tabela de destino** e clique **Editar SQL**. Digite a sintaxe CREATE TABLE para criar uma tabela com otimização de memória no banco de dados de destino. Clique em **OK** e conclua as etapas restantes no assistente.  
  
        -   Planos de manutenção. As tarefas de manutenção reorganizar índice e recriar índice não têm suporte nas tabelas com otimização de memória e nos respectivos índices. Portanto, quando um plano de manutenção para recriar e reorganizar índice for executado, as tabelas com otimização de memória e seus índices nos bancos de dados selecionados serão omitidas.  
  
             As estatísticas de atualização da tarefa de manutenção não têm suporte com uma verificação por amostra em tabelas com otimização de memória e seus índices. Desse modo, quando um plano de manutenção para estatísticas de atualização for executado, as estatísticas para tabelas com otimização de memória e seus índices serão sempre atualizadas para `WITH FULLSCAN, NORECOMPUTE`.  
  
-   Painel de detalhes do Pesquisador de Objetos  
  
-   Explorador de Modelos  
  
## <a name="unsupported-features-in-ssmanstudiofull"></a>Recursos sem suporte no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 Para objetos OLTP na memória, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não oferece suporte a recursos e operações que também não têm suporte no mecanismo de banco de dados.  
  
 Para obter mais informações sobre recursos sem suporte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [recursos de SQL Server com suporte](unsupported-sql-server-features-for-in-memory-oltp.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao SQL Server para OLTP na memória](sql-server-support-for-in-memory-oltp.md)  
  
  
