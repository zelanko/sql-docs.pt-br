---
title: Espelhamento de banco de dados e instantâneos do banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- snapshots [SQL Server database snapshots], database mirroring
- database snapshots [SQL Server], database mirroring
ms.assetid: 0bf1be90-7ce4-484c-aaa7-f8a782f57c5f
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d73770ada2435e0849df9b4604081580ef0c623f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115713"
---
# <a name="database-mirroring-and-database-snapshots-sql-server"></a>Espelhamento de banco de dados e instantâneos de banco de dados (SQL Server)
  Você pode tirar proveito de um banco de dados espelho que você está mantendo para fins de disponibilidade para descarregar relatórios. Para usar um banco de dados espelho para relatórios, você pode criar um instantâneo do banco de dados no banco de dados espelho e direcionar as solicitações de conexão de clientes para o instantâneo mais recente. Um instantâneo do banco de dados é um instantâneo consistente de transações, estático e somente leitura de seu banco de dados de origem tal como ele estava no momento da criação do instantâneo. Para criar um instantâneo do banco de dados em um banco de dados espelho, o banco de dados precisa estar no estado de espelhamento sincronizado.  
  
 Ao contrário do próprio banco de dados espelho, um instantâneo do banco de dados está acessível aos clientes. Contanto que o servidor espelho esteja se comunicando com o servidor principal, você pode dirigir os clientes que estejam inserindo informações para que se conectem a um instantâneo. Observe que devido ao fato de o instantâneo do banco de dados ser estático, os novos dados não estão disponíveis. Para tornar dados relativamente recentes disponíveis a seus usuários, você precisa criar periodicamente um novo instantâneo do banco de dados e fazer com que os aplicativos dirijam as conexões de entrada de clientes para o instantâneo mais recente.  
  
 Um novo instantâneo do banco de dados está quase vazio, mas cresce com o tempo, conforme mais e mais páginas do banco de dados são atualizadas pela primeira vez. Como todo instantâneo em um banco de dados cresce incrementalmente desse modo, cada instantâneo do banco de dados consome os mesmos recursos que um banco de dados normal. Dependendo das configurações do servidor espelho e do servidor principal, um número excessivo de instantâneos de banco de dados em um banco de dados espelho pode diminuir o desempenho no banco de dados principal. Portanto, recomendamos que você mantenha só alguns instantâneos relativamente recentes em seus bancos de dados espelhos. Geralmente, depois de criar um instantâneo de substituição, você deve redirecionar as entradas de consultas para o novo instantâneo e descartar o instantâneo mais antigo depois que as consultas atuais forem concluídas.  
  
> [!NOTE]  
>  Para obter mais informações sobre instantâneos de banco de dados, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
 Se houver troca de função, o banco de dados e seus instantâneos serão reinicializados, desconectando os usuários temporariamente. Depois, os instantâneos do banco de dados permanecem na instância de servidor em que foram criados e que se tornou o novo banco de dados principal. Os usuários podem continuar usando os instantâneos depois do failover. Porém, isso coloca uma carga adicional no novo servidor principal. Se o desempenho for uma preocupação em seu ambiente, recomendamos que você crie um instantâneo no novo banco de dados espelho quando ele se tornar disponível, redirecione os clientes ao novo instantâneo e descarte todos os instantâneos do banco de dados do antigo banco de dados espelho.  
  
> [!NOTE]  
>  Para uma solução de relatórios dedicada que seja bem dimensionável, pense em replicação. Para obter mais informações, consulte [Replicação do SQL Server](../install-windows/install-sql-server-replication.md).  
  
## <a name="example"></a>Exemplo  
 Esse exemplo cria instantâneos em um banco de dados espelho.  
  
 Suponha que o banco de dados de uma sessão de espelhamento de banco de dados seja [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Esse exemplo cria três instantâneos do banco de dados na cópia espelhada do banco de dados `AdventureWorks` que está na unidade `F` . Os instantâneos são nomeados `AdventureWorks_0600`, `AdventureWorks_1200`e `AdventureWorks_1800` para identificar seu horário aproximado de criação.  
  
1.  Crie o primeiro instantâneo do banco de dados no espelho de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
    ```  
    CREATE DATABASE AdventureWorks_0600  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_0600.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
2.  Crie o segundo instantâneo do banco de dados no espelho de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Os usuários que ainda estejam usando o `AdventureWorks_0600` podem continuar a usá-lo.  
  
    ```  
    CREATE DATABASE AdventureWorks_1200  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1200.SNP')  
       AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     Neste ponto, novas conexões de cliente podem ser direcionadas programaticamente para o instantâneo mais recente.  
  
3.  Crie o terceiro instantâneo do banco de dados no espelho [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Os usuários que ainda estejam usando o `AdventureWorks_0600` ou o `AdventureWorks_1200` podem continuar a usá-los.  
  
    ```  
    CREATE DATABASE AdventureWorks_1800  
    ON (NAME = 'datafile', FILENAME = 'F:\AdventureWorks_1800.SNP')  
        AS SNAPSHOT OF AdventureWorks2012  
    ```  
  
     Neste ponto, novas conexões de cliente podem ser direcionadas programaticamente para o instantâneo mais recente.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  

  
## <a name="see-also"></a>Consulte também  
 [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  