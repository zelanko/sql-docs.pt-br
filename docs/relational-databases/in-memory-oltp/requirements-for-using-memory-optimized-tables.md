---
title: Requisitos para usar tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: 65
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e08c8b1312c5aa9f0dac57195d937b12c94dca92
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="requirements-for-using-memory-optimized-tables"></a>Requisitos para usar tabelas com otimização de memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Para usar o OLTP in-memory no Banco de Dados do Azure, consulte [Introdução a Na Memória no Banco de Dados SQL](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  
 Além dos [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), estes são os requisitos para usar o OLTP in-memory:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 (ou posterior), qualquer edição. Para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM (pré SP1), você precisará da edição Enterprise, Developer ou Evaluation.
    
    > [!NOTE]
    > O OLTP in-memory exige a versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa de memória suficiente para manter os dados em tabelas e índices com otimização de memória, bem como memória adicional para dar suporte à carga de trabalho online. Consulte [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) para obter mais informações.  

-   Ao executar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma VM (máquina virtual), certifique-se de que haja memória suficiente alocada à VM para dar suporte à memória necessária para os índices e tabelas com otimização de memória. Dependendo do aplicativo host da VM, a opção de configuração para garantir a alocação de memória para a VM pode ser chamada de Reserva de Memória ou ao usar Memória Dinâmica, RAM Mínima. Verifique se essas configurações são suficientes para atender às necessidades dos bancos de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   O espaço livre em disco é duas vezes o tamanho das tabelas duráveis com otimização de memória.  
  
-   Um processador precisa dar suporte à instrução **cmpxchg16b** para usar o OLTP in-memory. Todos os processadores de 64 bits modernos dão suporte a **cmpxchg16b**.  
  
     Se você estiver usando um aplicativo host de máquina virtual e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir um erro causado por um processador mais antigo, verifique se o aplicativo host da VM tem uma opção de configuração para permitir **cmpxchg16b**. Caso contrário, você pode usar Hyper-V, que dá suporte a **cmpxchg16b** sem precisar modificar uma opção de configuração.  
  
-   O OLTP in-memory é instalado como parte dos **Serviços de Mecanismo de Banco de Dados**.  
  
     Para instalar a geração de relatórios ([Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) e o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (para gerenciar o OLTP in-memory por meio do Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), [baixe o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).   
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>Observações importantes sobre o uso do [!INCLUDE[hek_2](../../includes/hek-2-md.md)]  
  
-   A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], não há limite no tamanho das tabelas com otimização de memória que não seja a memória disponível. 

-   No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], o tamanho total da memória de todas as tabelas duráveis em um banco de dados não deve exceder 250 GB. Para obter mais informações, consulte [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).  

> [!NOTE]
> A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, as edições Standard e Express são compatíveis com a OLTP in-memory, mas elas impõem cotas na quantidade de memória que você pode usar para tabelas com otimização de memória em um determinado banco de dados. Na Standard Edition são 32 GB por banco de dados; na Express Edition são 352 MB por banco de dados. 
  
-   Se criar um ou vários bancos de dados com tabelas com otimização de memória, você deverá habilitar a IFI (Inicialização Imediata de Arquivo) ao conceder à conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o direito de usuário *SE_MANAGE_VOLUME_NAME*. Sem a IFI, os arquivos de armazenamento com otimização de memória (arquivos delta e de dados) serão inicializados após a criação, o que pode ter um impacto negativo no desempenho de sua carga de trabalho. Para obter mais informações sobre a IFI, inclusive sobre como habilitá-la, consulte [Inicialização imediata de arquivo do banco de dados](../../relational-databases/databases/database-instant-file-initialization.md).
  
## <a name="see-also"></a>Consulte Também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
 [Inicialização imediata de arquivo do banco de dados](../../relational-databases/databases/database-instant-file-initialization.md)  
 [Guia de arquitetura de memória](../../relational-databases/memory-management-architecture-guide.md)
  
