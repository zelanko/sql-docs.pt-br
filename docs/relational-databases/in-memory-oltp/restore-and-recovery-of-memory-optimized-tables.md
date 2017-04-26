---
title: "Restauração e recuperação de tabelas com otimização de memória | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 56e6ac814b90fdd38f21be32f506846e542be977
ms.lasthandoff: 04/11/2017

---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Restauração e recuperação de tabelas com otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  O mecanismo básico para recuperar ou restaurar um banco de dados com tabelas com otimização de memória é semelhante a bancos de dados com apenas tabelas baseadas em disco. Mas, de modo diferente das tabelas baseadas em disco, as tabelas com otimização de memória devem ser carregadas na memória antes que o banco de dados seja disponibilizado para o acesso de usuários. Isso adiciona uma nova etapa na recuperação do banco de dados.  
  
 Durante as operações de recuperação ou restauração, o mecanismo OLTP na memória lê os arquivos delta e de dados para carregamento na memória física. O tempo de carregamento é determinado pelos seguintes fatores:  
  
-   A quantidade de dados a serem carregados.  
  
-   Largura de banda de E/S sequencial.  
  
-   Grau de paralelismo, determinado pelo número de contêineres de arquivo e núcleos de processador.  
  
-   A quantidade de registros de log na parte ativa do log que precisam ser refeitos.  
  
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
  
 ![Tabelas com otimização de memória. ](../../relational-databases/in-memory-oltp/media/memory-optimized-tables.gif "Tabelas com otimização de memória.")  
  
 As tabelas com otimização de memória normalmente podem ser carregadas na memória na velocidade de E/S, mas, em alguns casos, o carregamento de linhas de dados será mais lento. Os casos específicos são:  
  
-   O baixo número de buckets para o índice de hash pode levar à colisão excessiva, causando lentidão nas inserções de linhas de dados. Em geral, isso resulta na alta utilização da CPU como um todo, especialmente no final da recuperação. Se você configurou o índice de hash corretamente, ele não deve afetar o tempo de recuperação.  
  
-   Tabelas grandes com otimização de memória, com um ou mais índices não clusterizados, são diferentes de um índice de hash cujo número de buckets é dimensionado no momento de criação. Os índices não clusterizados crescem dinamicamente, resultando na alta utilização da CPU.  
  
## <a name="see-also"></a>Consulte também  
 [Backup, restauração e recuperação de tabelas com otimização de memória](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
