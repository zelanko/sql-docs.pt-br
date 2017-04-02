---
title: "O grupo de arquivos com otimiza&#231;&#227;o de mem&#243;ria | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# O grupo de arquivos com otimiza&#231;&#227;o de mem&#243;ria
  Para criar tabelas com otimização de memória, você deve primeiro criar um grupo de arquivos com otimização de memória. O grupo de arquivos com otimização de memória retém um ou mais contêineres. Cada contêiner contém arquivos de dados ou arquivos delta, ou então ambos.  
  
 Embora as linhas de dados das tabelas SCHEMA_ONLY não persistam e os metadados para tabelas otimizadas para memória e procedimentos armazenados compilados nativamente estejam armazenados nos catálogos tradicionais, o mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ainda requer um grupo de arquivos com otimização de memória para tabelas otimizadas para memória SCHEMA_ONLY para fornecer uma experiência uniforme para bancos de dados com tabelas otimizadas para memória.  
  
 O grupo de arquivos com otimização de memória baseia-se no grupo de arquivos do fluxo de arquivos, com as seguintes diferenças:  
  
-   Só é possível criar um grupo de arquivos com otimização de memória por banco de dados. É necessário marcar explicitamente o grupo de arquivos como contendo o memory_optimized_data. Você pode criar o grupo de arquivos ao criar o banco de dados ou poderá adicioná-lo posteriormente:  
  
    ```  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   é necessário adicionar um ou mais contêineres ao grupo de arquivos MEMORY_OPTIMIZED_DATA. Por exemplo:  
  
    ```  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Não é necessário habilitar o fluxo de arquivos ([Habilitar e configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)) para criar um grupo de arquivos com otimização de memória. O mapeamento do fluxo de arquivos é realizado pelo mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
-   Você pode adicionar novos contêineres a um grupo de arquivos com otimização de memória. Você pode precisar de um novo contêiner para expandir o armazenamento necessário para a tabela otimizada para memória e também para distribuir ES entre vários contêineres.  
  
-   O movimento dos dados com um grupo de arquivos com otimização de memória é otimizado em uma configuração do Grupo de Disponibilidade AlwaysOn. Diferente dos arquivos do fluxo de arquivos enviados para as réplicas secundárias, os arquivos de ponto de verificação (tanto de dados quanto de delta) no grupo de arquivos com otimização de memória não são enviados para as réplicas secundárias. Os arquivos de dados e delta são criados usando o log de transação na réplica secundária.  
  
 As limitações a seguir do grupo de arquivos com otimização de memória,  
  
-   Depois de criar um grupo de arquivos com otimização de memória, você somente poderá removê-lo ao descartar o banco de dados. Em um ambiente de produção, é muito improvável que você precise remover o grupo de arquivos com otimização de memória.  
  
-   Não é possível descartar um contêiner não vazio ou mover os pares de dados e arquivo delta para outro contêiner no grupo de arquivos com otimização de memória.  
  
-   Não é possível especificar o MAXSIZE para o contêiner.  
  
## Configurando um grupo de arquivos com otimização de memória  
 Considere criar múltiplos contêineres em um grupo de arquivos com otimização de memória e distribui-los em diferentes unidades para obter mais largura de banda para transferir os dados para a memória.  
  
 Ao configurar o armazenamento, é necessário fornecer espaço livre em disco de quatro vezes o tamanho das tabelas com otimização de memória. Também é necessário garantir que o subsistema de ES suporte o IOPS para a carga de trabalho. Se os pares de dados e arquivo delta forem populados em um IOPS específico, será necessário três vezes o tamanho do IOPS para abranger as operações de armazenamento e mesclagem. Você pode adicionar capacidade de armazenamento e IOPS adicionando um ou mais contêineres ao grupo de arquivos com otimização de memória.  
  
## Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  