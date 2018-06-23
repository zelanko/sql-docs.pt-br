---
title: Restauração e recuperação de tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: c4ceab3fcf30c6709a5cfd4138c717d4c3153a05
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120785"
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Restauração e recuperação de tabelas com otimização de memória
  O mecanismo básico para recuperar ou restaurar um banco de dados com tabelas com otimização de memória é semelhante a bancos de dados com apenas tabelas baseadas em disco. Mas, de modo diferente das tabelas baseadas em disco, as tabelas com otimização de memória devem ser carregadas na memória antes que o banco de dados seja disponibilizado para o acesso de usuários. Isso adiciona uma nova etapa na recuperação do banco de dados. As etapas modificadas na recuperação do banco de dados são alteradas como segue:  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado, cada banco de dados passa por uma fase de recuperação que consiste em três fases:  
  
1.  A fase de análise. Durante essa fase, verificam-se os logs de transações ativas para detectar transações confirmadas e não confirmadas. O mecanismo de OLTP na memória identifica o ponto de verificação para carregamento e pré-carrega suas entradas de log da tabela do sistema. Ele também processa alguns registros de log de alocação de arquivo.  
  
2.  A fase refazer. Essa fase é executada simultaneamente em tabelas baseadas em disco e com otimização de memória.  
  
     Para tabelas baseadas em disco, o banco de dados é movido para o momento atual e adquire bloqueios usados por transações não confirmadas.  
  
     Para tabelas com otimização de memória, os dados dos pares de arquivos de dados e delta são carregados na memória. Depois, eles atualizam os dados com o log de transações ativas baseado no último ponto de verificação durável.  
  
     Quando as operações acima em tabelas baseadas em disco e com otimização de memória são concluídas, o banco de dados está disponível para acesso.  
  
3.  A fase desfazer. Nessa fase, as transações não confirmadas são revertidas.  
  
 Carregar tabelas com otimização de memória na memória pode afetar o desempenho do RTO (objetivo de tempo de recuperação). Para melhorar o tempo de carregamento dos dados com otimização de memória em arquivos de dados e delta, o mecanismo OLTP na memória carrega os arquivos de dados/delta em paralelo desta forma:  
  
-   Criando um filtro de mapa delta. Referências de repositórios de arquivos delta para as linhas excluídas. Um thread por contêiner lê os arquivos delta e cria um filtro de mapa delta. (Um grupo de arquivos de dados com otimização de memória pode ter um ou mais contêineres.)  
  
-   Transmitindo os arquivos de dados.  Após a criação do filtro de mapa de delta, os arquivos de dados são lidos usando o número de threads que corresponde às CPUs lógicas existentes. Cada thread que lê o arquivo de dados lê as linhas de dados, verifica o mapa delta associado, e só insere a linha na tabela se essa linha não foi marcada como excluída. Esta parte da recuperação pode estar associada à CPU em alguns casos, conforme observado a seguir.  
  
 ![Tabelas com otimização de memória. ](../../database-engine/media/memory-optimized-tables.gif "Tabelas com otimização de memória.")  
  
 As tabelas com otimização de memória normalmente podem ser carregadas na memória na velocidade de E/S, mas, em alguns casos, o carregamento de linhas de dados será mais lento. Os casos específicos são:  
  
-   O baixo número de buckets para o índice de hash pode levar à colisão excessiva, causando lentidão nas inserções de linhas de dados. Em geral, isso resulta na alta utilização da CPU como um todo, especialmente no final da recuperação. Se você configurou o índice de hash corretamente, ele não deve afetar o tempo de recuperação.  
  
-   Tabelas grandes com otimização de memória, com um ou mais índices não clusterizados, são diferentes de um índice de hash cujo número de buckets é dimensionado no momento de criação. Os índices não clusterizados crescem dinamicamente, resultando na alta utilização da CPU.  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>Restaurando um Banco de dados com tabelas com otimização de memória  
 Você sabe que tem memória suficiente no servidor para restaurar um banco de dados, mas há um requisito de memória necessária para o banco de dados que é contabilizada como parte de um Pool de recursos existente.  Você sabe que não é possível criar a associação ao pool de recursos antes de o banco de dados existir, para que você execute a restauração WITH NORECOVERY.  Isso faz com que a imagem de disco do banco de dados seja restaurada e o banco de dados seja criado, mas nenhuma memória de OLTP na memória é consumida, porque o banco de dados não é colocado online.  
  
 Neste ponto, você pode criar o Pool de Recursos fazendo a associação do Banco de dados e, em seguida, usar RESTORE WITH RECOVERY para colocar o banco de dados restaurado online.  Assim que a associação estiver em vigor, antes de o banco de dados ser colocado online, o seu consumo de memória do OLTP na memória é contabilizado corretamente. Isso requer que o banco de dados seja restaurado apenas uma vez. O primeiro comando RESTORE é um comando informativo que lê apenas o cabeçalho do backup e o último comando simplesmente aciona a recuperação sem, de fato, restaurar qualquer bit.  
  
## <a name="see-also"></a>Consulte também  
 [Backup, restauração e recuperação de tabelas com otimização de memória](memory-optimized-tables.md)  
  
  