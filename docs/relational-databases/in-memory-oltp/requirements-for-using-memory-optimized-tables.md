---
title: "Requisitos para usar tabelas com otimização de memória | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: 65
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d30c5b808c13258e784187182eab23b0a50c76e0
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="requirements-for-using-memory-optimized-tables"></a>Requisitos para usar tabelas com otimização de memória
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Para usar o OLTP in-memory no Banco de Dados do Azure, consulte [Introdução a Na Memória no Banco de Dados SQL](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  
 Além dos [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), estes são os requisitos para usar o OLTP in-memory:  
  
-   SQL Server 2016 SP1 (ou posterior), qualquer edição. Para o SQL Server 2014 e SQL Server 2016 RTM (pré-SP1), você precisa da edição Enterprise, Developer ou Evaluation.
    - Observação: o OLTP na memória requer a versão de 64 bits do SQL Server.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa de memória suficiente para manter os dados em tabelas e índices com otimização de memória, bem como memória adicional para dar suporte à carga de trabalho online. Consulte [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) para obter mais informações.  

-   Ao executar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma VM (máquina virtual), certifique-se de que haja memória suficiente alocada à VM para dar suporte à memória necessária para os índices e tabelas com otimização de memória. Dependendo do aplicativo host da VM, a opção de configuração para garantir a alocação de memória para a VM pode ser chamada de Reserva de Memória ou ao usar Memória Dinâmica, RAM Mínima. Verifique se essas configurações são suficientes para atender às necessidades dos bancos de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   O espaço livre em disco é duas vezes o tamanho das tabelas duráveis com otimização de memória.  
  
-   Um processador precisa dar suporte à instrução **cmpxchg16b** para usar o OLTP in-memory. Todos os processadores de 64 bits modernos dão suporte a **cmpxchg16b**.  
  
     Se você estiver usando um aplicativo host de máquina virtual e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir um erro causado por um processador mais antigo, verifique se o aplicativo host da VM tem uma opção de configuração para permitir **cmpxchg16b**. Caso contrário, você pode usar Hyper-V, que dá suporte a **cmpxchg16b** sem precisar modificar uma opção de configuração.  
  
-   O OLTP in-memory é instalado como parte dos **Serviços de Mecanismo de Banco de Dados**.  
  
     Para instalar a geração de relatórios ([Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (para gerenciar o OLTP in-memory por meio do Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ), [Baixar o SSMS (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx).  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>Observações importantes sobre o uso do [!INCLUDE[hek_2](../../includes/hek-2-md.md)]  
  
-   A partir do SQL Server 2016, não há limite no tamanho das tabelas com otimização de memória que não seja a memória disponível. No SQL Server 2014, o tamanho total na memória de todas as tabelas duráveis em um banco de dados não deve exceder 250 GB para bancos de dados do SQL Server 2014. Para obter mais informações, consulte [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).  
    - Observação: a partir do SQL Server 2016 SP1, a Standard Edition e a Express Edition oferecem suporte a OLTP na memória, mas elas impõem cotas na quantidade de memória que você pode usar para tabelas com otimização de memória em um determinado banco de dados. Na Standard Edition são 32 GB por banco de dados; na Express Edition são 352 MB por banco de dados. 
  
-   Se você criar um ou vários bancos de dados com tabelas com otimização de memória, deverá habilitar a inicialização imediata de arquivo (conceda à conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o direito de usuário SE_MANAGE_VOLUME_NAME) para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sem a inicialização imediata de arquivo, os arquivos de armazenamento com otimização de memória (arquivos delta e de dados) serão inicializados após a criação, que pode ter um impacto negativo no desempenho de sua carga de trabalho. Para obter mais informações sobre a inicialização imediata de arquivo, consulte [Inicialização de arquivo de banco de dados](http://msdn.microsoft.com/library/ms175935\(SQL.105\).aspx). Para obter informações sobre como habilitar a inicialização imediata de arquivo, consulte [Como e por que habilitar a inicialização imediata de arquivo](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx).  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

