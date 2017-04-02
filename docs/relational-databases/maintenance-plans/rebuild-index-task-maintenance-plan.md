---
title: "Tarefa Recriar &#205;ndice (Plano de Manuten&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "reindex"
  - "sql13.swb.maint.reindex.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Tarefa Recriar Índice"
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
caps.latest.revision: 42
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 42
---
# Tarefa Recriar &#205;ndice (Plano de Manuten&#231;&#227;o)
  Use a caixa de diálogo **Tarefa Recompilar Índice** para recriar os índices nas tabelas do banco de dados com um novo fator de preenchimento. O fator de preenchimento determina a quantidade de espaço vazio em cada página no índice, para acomodar futuras expansões. À medida que os dados são adicionados à tabela, o espaço livre é todo preenchido porque o fator de preenchimento não é mantido. Reorganizando dados e páginas de índice, é possível restabelecer o espaço livre.  
  
 A **Tarefa Recompilar Índice** usa a instrução ALTER INDEX. Para obter mais informações sobre as opções descritas nesta página, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
## Opções  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Nova**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Bancos de dados**  
 Especifique os bancos de dados afetados por essa tarefa.  
  
-   **Todos os bancos de dados**  
  
     Gere um plano de manutenção que executa tarefas de manutenção em todos os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto o tempdb.  
  
-   **Todos os bancos de dados do sistema**  
  
     Gera um plano de manutenção que execute tarefas de manutenção em cada banco de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto o tempdb. Nenhuma tarefa de manutenção é executada nos bancos de dados criados pelo usuário.  
  
-   **Todos os bancos de dados de usuários**  
  
     Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados criados por usuários. Nenhuma tarefa de manutenção é executada com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Estes bancos de dados específicos**  
  
     Gere um plano de manutenção que execute tarefas de manutenção somente nos bancos de dados selecionados. Pelo menos um banco de dados da lista deverá ser selecionado se esta opção for escolhida.  
  
    > [!NOTE]  
    >  Os planos de manutenção são executados somente em bancos de dados definidos com nível de compatibilidade 80 ou superior. Os bancos de dados definidos para o nível de compatibilidade 70 ou inferior não são exibidos.  
  
 **Objeto**  
 Limita a grade **Seleção** para exibir tabelas, exibições ou ambas.  
  
 **Selection**  
 Especifique as tabelas ou índices afetados por esta tarefa. Não disponível quando **Tabelas e Exibições** estiver selecionado na caixa Objeto.  
  
 **Espaço livre padrão por página**  
 Descarta os índices nas tabelas no banco de dados e recria-os com o fator de preenchimento especificado quando os índices foram criados.  
  
 **Alterar espaço livre por página**  
 Descarta os índices nas tabelas no banco de dados e recria-os com um fator de preenchimento novo, calculado automaticamente, reservando a quantidade especificada de espaço livre nas páginas de índice. Quanto maior a porcentagem, mais espaço livre será reservado nas páginas de índice e maior ficará o índice. Os valores válidos são de 0 a 100.  
  
 **Classificar resultados no tempdb**  
 Use a opção `SORT_IN_TEMPDB`, que determina onde os resultados intermediários da classificação, gerados durante a criação do índice, são armazenados temporariamente. Se uma operação de classificação não for necessária ou se a classificação puder ser executada na memória, a opção `SORT_IN_TEMPDB`será ignorada.  
  
 **Preenchimento de índice**  
 Especificar o preenchimento do índice  
  
 **Manter o índice online**  
 Use a opção `ONLINE`, que permite o acesso de usuários aos dados da tabela subjacente ou de índice clusterizado e qualquer índice não clusterizado associado durante as operações de índice.  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
 **Não recompilar índices | Recompilar índices offline**  
 Especifique o que fazer com os tipos de índice que não podem ser recompilados enquanto estão online.  
  
 **MAXDOP**  
 Especifique um valor para limitar o número de processadores usados em uma execução de plano paralelo.  
  
 **Baixa Prioridade Usada**  
 Escolha esta opção para aguardar os bloqueios de baixa prioridade.  
  
 **Anular após Esperar**  
 Especifique o que fazer após o tempo especificado por **Duração Máxima** ter transcorrido.  
  
 **Duração Máxima**  
 Especifique o tempo de espera para os bloqueios de baixa prioridade.  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **Atualizar**  
 Atualize a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com a Autenticação do Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte-se com uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## Consulte também  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)   
 [Diretrizes para operações de índice online](../../relational-databases/indexes/guidelines-for-online-index-operations.md)   
 [Como funcionam as operações de índice online](../../relational-databases/indexes/how-online-index-operations-work.md)   
 [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)  
  
  