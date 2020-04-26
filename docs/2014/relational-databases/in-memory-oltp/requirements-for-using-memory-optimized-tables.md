---
title: Requisitos para usar tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b9e442fb97245d32c398602cdfd727de8239cb8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62467882"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>Requisitos para usar tabelas com otimização de memória
  Além dos requisitos de [hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), veja a seguir os requisitos para usar o OLTP na memória:  
  
-   Enterprise, Developer ou Evaluation edition de 64 bits do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa de memória suficiente para manter os dados nas tabelas e índices com otimização de memória. Para considerar versões de linha, você deve fornecer uma quantidade de memória duas vezes maior que o tamanho esperado de tabelas e índices com otimização de memória. Mas a quantidade real de memória necessária dependerá da carga de trabalho. Você deve monitorar o uso de memória e fazer ajustes quando necessário. O tamanho dos dados nas tabelas com otimização de memória não deve exceder a porcentagem permitida do pool. Para descobrir o tamanho de uma tabela com otimização de memória, consulte [Sys. dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql).  
  
     Se você tiver tabelas baseadas em disco no banco de dados, precisará fornecer memória suficiente para o pool de buffers e o processamento de consulta nessas tabelas.  
  
     É importante saber quanto de memória seu aplicativo OLTP na memória exigirá. Consulte [Estimar requisitos de memória para tabelas com otimização de memória](memory-optimized-tables.md) para obter mais informações.  
  
-   O espaço livre em disco é duas vezes o tamanho das tabelas duráveis com otimização de memória.  
  
-   Um processador precisa dar suporte à instrução **cmpxchg16b** para usar o OLTP in-memory. Todos os processadores de 64 bits modernos dão suporte a **cmpxchg16b**.  
  
     Se você estiver usando um aplicativo host de VM e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir um erro causado por um processador mais antigo, verifique se o aplicativo tem uma opção de configuração para permitir **cmpxchg16b**. Caso contrário, você pode usar Hyper-V, que dá suporte a **cmpxchg16b** sem precisar modificar uma opção de configuração.  
  
-   Para instalar OLTP na memória, selecione **Serviços de Mecanismo de Banco de Dados** ao instalar o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
     Para instalar a geração de relatórios ([determinando se uma tabela ou um procedimento armazenado deve ser movido para OLTP na memória](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e (para gerenciar o OLTP na [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] memória por meio do pesquisador de objetos), selecione **ferramentas de gerenciamento-básicas** ou [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] **ferramentas de gerenciamento-avançadas** ao instalar o.  
  
## <a name="important-notes-on-using-hek_2"></a>Observações importantes sobre o uso do [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]  
  
-   O tamanho total da memória de todas as tabelas duráveis em um banco de dados não deve exceder 250 GB. Para obter mais informações, consulte [durabilidade para tabelas com otimização de memória](durability-for-memory-optimized-tables.md).  
  
-   Esta versão do [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] é direcionada para executar de forma otimizada em sistemas com 2 ou 4 soquetes e menos de 60 núcleos.  
  
-   Os arquivos de ponto de verificação não devem ser excluídos manualmente. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa automaticamente a coleta de lixo em arquivos de ponto de verificação desnecessários. Para obter mais informações, consulte a discussão sobre mesclagem de dados e arquivos Delta em [durabilidade para tabelas com otimização de memória](durability-for-memory-optimized-tables.md).  
  
-   Na primeira versão do OLTP na memória (no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]), a única maneira de remover um grupo de arquivos com otimização de memória é descartar o banco de dados.  
  
-   Se você tentar excluir um lote grande de linhas enquanto há uma inserção ou atualização de carga de trabalho simultânea afetando o intervalo de linhas que você está tentando excluir, a exclusão poderá falhar. A solução alternativa é interromper a inserção ou atualização da carga de trabalho antes de fazer a exclusão. Como alternativa, você pode configurar a transação em transações menores, que seriam menos prováveis de serem corrompidas por uma carga de trabalho simultânea. Como ocorre com todas as operações de gravação em tabelas com otimização de memória, use a lógica de repetição ([Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)).  
  
-   Se você criar um ou vários bancos de dados com tabelas com otimização de memória, deverá habilitar a inicialização imediata de arquivo (conceda à conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o direito de usuário SE_MANAGE_VOLUME_NAME) para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sem a inicialização imediata de arquivo, os arquivos de armazenamento com otimização de memória (arquivos delta e de dados) serão inicializados após a criação, que pode ter um impacto negativo no desempenho de sua carga de trabalho. Para obter mais informações sobre a inicialização imediata de arquivo, consulte [Inicialização de arquivo de banco de dados](../databases/database-instant-file-initialization.md). Para obter informações sobre como habilitar a inicialização imediata de arquivo, consulte [Como e por que habilitar a inicialização imediata de arquivo](https://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx).  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos ouvindo  
 Quais são as informações que você está procurando? Você as localizou? Estamos ouvindo seus comentários para melhorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page).  
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
