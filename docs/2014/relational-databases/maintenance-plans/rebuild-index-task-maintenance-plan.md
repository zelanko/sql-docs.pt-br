---
title: Tarefa Recompilar Índice (plano de manutenção) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reindex.f1
- reindex
helpviewer_keywords:
- Rebuild Index Task dialog box
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34bd5a607998c6e37f688ccbadcd4d612d3daea7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62806978"
---
# <a name="rebuild-index-task-maintenance-plan"></a>Tarefa Recriar Índice (Plano de Manutenção)
  Use a caixa de diálogo **Tarefa Recompilar Índice** para recriar os índices nas tabelas do banco de dados com um novo fator de preenchimento. O fator de preenchimento determina a quantidade de espaço vazio em cada página no índice, para acomodar futuras expansões. À medida que os dados são adicionados à tabela, o espaço livre é todo preenchido porque o fator de preenchimento não é mantido. Reorganizando dados e páginas de índice, é possível restabelecer o espaço livre.  
  
 A **Tarefa Recompilar Índice** usa a instrução ALTER INDEX.  
  
## <a name="options"></a>Opções  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Novo**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Bancos de dados**  
 Especifique os bancos de dados afetados por essa tarefa.  
  
-   **Todos os bancos de dados**  
  
     Gere um plano de manutenção que executa tarefas de manutenção em todos os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto o tempdb.  
  
-   **Todos os bancos de dados do sistema**  
  
     Gera um plano de manutenção que execute tarefas de manutenção em cada banco de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , exceto o tempdb. Nenhuma tarefa de manutenção é executada nos bancos de dados criados pelo usuário.  
  
-   **Todos os bancos de dados de usuários**  
  
     Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados criados por usuários. Nenhuma tarefa de manutenção é executada com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Estes bancos de dados específicos**  
  
     Gere um plano de manutenção que execute tarefas de manutenção somente nos bancos de dados selecionados. Pelo menos um banco de dados da lista deverá ser selecionado se esta opção for escolhida.  
  
    > [!NOTE]  
    >  Os planos de manutenção são executados somente em bancos de dados definidos com nível de compatibilidade 80 ou superior. Os bancos de dados definidos para o nível de compatibilidade 70 ou inferior não são exibidos.  
  
 **Objeto**  
 Limita a grade **Seleção** para exibir tabelas, exibições ou ambas.  
  
 **Seleção**  
 Especifique as tabelas ou índices afetados por esta tarefa. Não disponível quando **Tabelas e Exibições** estiver selecionado na caixa Objeto.  
  
 **Reorganiza páginas com a quantidade padrão de espaço livre**  
 Descarta os índices nas tabelas no banco de dados e recria-os com o fator de preenchimento especificado quando os índices foram criados.  
  
 **Alterar o espaço livre por porcentagem de página para**  
 Descarta os índices nas tabelas no banco de dados e recria-os com um fator de preenchimento novo, calculado automaticamente, reservando a quantidade especificada de espaço livre nas páginas de índice. Quanto maior a porcentagem, mais espaço livre será reservado nas páginas de índice e maior ficará o índice. Os valores válidos são de 0 a 100.  
  
 **Classificar resultados no tempdb**  
 Use a `SORT_IN_TEMPDB`opção, que determina onde os resultados intermediários de classificação, gerados durante a criação do índice, são armazenados temporariamente. Se uma operação de classificação não for necessária ou se a classificação puder ser executada na memória, a opção `SORT_IN_TEMPDB`será ignorada.  
  
 **Mantenha o índice online enquanto reindexa**  
 Use a opção `ONLINE` , que permite o acesso de usuários aos dados da tabela subjacente ou de índice clusterizado e qualquer índice não clusterizado associado durante as operações de índice.  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## <a name="new-connection-dialog-box"></a>Caixa de diálogo Nova Conexão  
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
 Conecte-se com uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [Opção SORT_IN_TEMPDB para índices](../indexes/indexes.md)   
 [Diretrizes para operações de índice online](../indexes/guidelines-for-online-index-operations.md)   
 [Como funcionam as operações de índice online](../indexes/how-online-index-operations-work.md)   
 [Executar operações de índice online](../indexes/perform-index-operations-online.md)  
  
  
