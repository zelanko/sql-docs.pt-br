---
title: O grupo de arquivos com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 64402f73fdf43c0ebcbeff338ed72d56d55227be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155577"
---
# <a name="the-memory-optimized-filegroup"></a>O grupo de arquivos com otimização de memória
  Para criar tabelas com otimização de memória, você deve primeiro criar um grupo de arquivos com otimização de memória. O grupo de arquivos com otimização de memória retém um ou mais contêineres. Cada contêiner contém arquivos de dados ou arquivos delta, ou então ambos.  
  
 Embora as linhas de dados das tabelas `SCHEMA_ONLY` não persistam e os metadados para tabelas otimizadas para memória e procedimentos armazenados compilados nativamente estejam armazenados nos catálogos tradicionais, o mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ainda requer um grupo de arquivos com otimização de memória para tabelas otimizadas para memória `SCHEMA_ONLY` para fornecer uma experiência uniforme para bancos de dados com tabelas otimizadas para memória.  
  
 O grupo de arquivos com otimização de memória baseia-se no grupo de arquivos do fluxo de arquivos, com as seguintes diferenças:  
  
-   Só é possível criar um grupo de arquivos com otimização de memória por banco de dados. É necessário marcar explicitamente o grupo de arquivos como contendo o memory_optimized_data. Você pode criar o grupo de arquivos ao criar o banco de dados ou poderá adicioná-lo posteriormente:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   é necessário adicionar um ou mais contêineres ao grupo de arquivos MEMORY_OPTIMIZED_DATA. Por exemplo:   
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Não é necessário habilitar o fluxo de arquivos ([Habilitar e configurar FILESTREAM](../blob/enable-and-configure-filestream.md)) para criar um grupo de arquivos com otimização de memória. O mapeamento do fluxo de arquivos é realizado pelo mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   Você pode adicionar novos contêineres a um grupo de arquivos com otimização de memória. Talvez seja necessário um novo contêiner para expandir o armazenamento necessário para a tabela durável com otimização de memória e também para distribuir a e/s em vários contêineres.  
  
-   O movimento dos dados com um grupo de arquivos com otimização de memória é otimizado em uma configuração do Grupo de Disponibilidade AlwaysOn. Diferente dos arquivos do fluxo de arquivos enviados para as réplicas secundárias, os arquivos de ponto de verificação (tanto de dados quanto de delta) no grupo de arquivos com otimização de memória não são enviados para as réplicas secundárias. Os arquivos de dados e delta são criados usando o log de transação na réplica secundária.  
  
As limitações a seguir do grupo de arquivos com otimização de memória,  
  
-   Depois de criar um grupo de arquivos com otimização de memória, você somente poderá removê-lo ao descartar o banco de dados. Em um ambiente de produção, é muito improvável que você precise remover o grupo de arquivos com otimização de memória.  
  
-   Não é possível descartar um contêiner não vazio ou mover os pares de dados e arquivo delta para outro contêiner no grupo de arquivos com otimização de memória.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurando um grupo de arquivos com otimização de memória  
Considere criar múltiplos contêineres em um grupo de arquivos com otimização de memória e distribui-los em diferentes unidades para obter mais largura de banda para transferir os dados para a memória.  
  
Ao configurar o armazenamento, é necessário fornecer espaço livre em disco de quatro vezes o tamanho das tabelas com otimização de memória. Certifique-se de que seu subsistema de e/s suporta o IOPS necessário para sua carga de trabalho. Se os pares de dados e arquivo delta forem preenchidos em um IOPS específico, será necessário três vezes o tamanho do IOPS para abranger as operações de armazenamento e mesclagem. Você pode adicionar capacidade de armazenamento e IOPS adicionando um ou mais contêineres ao grupo de arquivos com otimização de memória.  
  
Em um contêiner múltiplo, cenário com várias unidades, os arquivos de dados e delta são alocados em rodízio nos contêineres. O primeiro arquivo de dados é alocado no primeiro contêiner e o arquivo delta é alocado no próximo contêiner, repetindo o padrão de alocação. Este esquema de alocação distribui os dados e os arquivos delta uniformemente entre os contêineres se você possui um arquivo ímpar de unidades, cada um mapeado para um contêiner. Contudo, se você possuir um número par de unidades, cada um mapeado para um contêiner, isso poderá resultar no armazenamento desequilibrado dos dados para unidades ímpares e arquivos deltas mapeados para unidades pares. Para obter um fluxo equilibrado de e/s na recuperação, considere posicionar pares de arquivos de dados e delta nos mesmos eixos/armazenamentos, conforme descrito no exemplo a seguir.  

> [!CAUTION]
> Se um `MAXSIZE` valor está definido para o grupo de arquivos com otimização de memória e arquivos de ponto de verificação excedem o tamanho máximo do contêiner, o banco de dados se torna suspeito.   
> Nesse caso, não tente definir o banco de dados como OFFLINE e ONLINE, fazendo o banco de dados permanecer no estado RECOVERY_PENDING.
  
### <a name="example"></a>Exemplo 
Considere um grupo de arquivos com otimização de memória com dois contêineres: o contêiner 1 na unidade X e o contêiner 2 nas unidades Y.  
Visto que a alocação dos arquivos de dados e delta é realizada em rodízio, o contêiner 1 somente possuirá os arquivos de dados, enquanto o contêiner 2 possuirá somente arquivos delta, o que levará ao desequilíbrio do armazenamento bem como das operações de entrada e saída por segundo, pois os arquivos de dados são significativamente maiores que os arquivos delta.    
Para distribuir arquivos de dados e delta uniformemente entre unidades X e Y, crie quatro contêineres em vez de dois e mapeie os primeiros dois contêineres a unidade X e os próximos dois contêineres para a unidade Y.  
Com alocação round-robin, os dados primeiro e o primeiro arquivo delta serão alocados no contêiner-1 e contêiner-2 respectivamente, que é mapeado para a unidade X.   
Da mesma forma, o próximo arquivo de dados e delta será alocado no contêiner-3 e contêiner-4, que são mapeados para a unidade Y. Isso permite distribuir os arquivos de dados e delta uniformemente entre as duas unidades.  
 
  
## <a name="see-also"></a>Consulte também  
[Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)     
[Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)    
  
