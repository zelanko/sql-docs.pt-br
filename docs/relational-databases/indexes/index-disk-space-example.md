---
title: "Exemplo de espaço em disco de índice | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34ea623f3e64833c73f23a5be78fd3cf9ef9722b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="index-disk-space-example"></a>Exemplo de espaço em disco de índice
  Sempre que um índice é criado, recriado, ou cancelado, o espaço em disco tanto para a velha (fonte) quanto para a nova (destino) estrutura é necessário em seus arquivos e grupos de arquivos apropriados. A estrutura antiga não é desalocada até que a transação de criação do índice seja confirmada. Pode igualmente ser necessário espaço temporário em disco adicional, para classificação de operações. Para obter mais informações, consulte [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
 Neste exemplo, os requisitos de espaço em disco para criar um índice clusterizado são determinados.  
  
 Suponha que as condições a seguir são verdadeiras antes de criar o índice cluster:  
  
-   A tabela existente (heap) contém 1 milhão de linhas. Cada linha tem 200 bytes de comprimento.  
  
-   O índice não clusterizados A contém 1 milhão de linhas. Cada linha tem 50 bytes de comprimento.  
  
-   O índice não clusterizados B contém 1 milhão de linhas. Cada linha tem 80 bytes de comprimento.  
  
-   A opção index create memory é definida como 2 MB.  
  
-   Um valor de fator de preenchimento de 80 é usado para todos os índices existentes e novos. Isto significa que as páginas estão preenchidas em 80 por cento.  
  
    > [!NOTE]  
    >  Como resultado da criação de um índice cluster, os dois índices não clusterizados devem ser reconstruídos para substituir o indicador de linha com a nova chave de índice clusterizado.  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>Cálculos de espaço em disco para uma operação de índice offline  
 Nos passos a seguir, são calculados tanto o espaço em disco temporário a ser usado durante a operação de índice quanto o espaço em disco permanente para armazenar novos índices. Os cálculos mostrados são aproximados; os resultados são arredondados e consideram apenas o tamanho do nível folha de índice. O til (~) é usado para indicar cálculos aproximados.  
  
1.  Determine o tamanho das estruturas de origem.  
  
     Heap: 1 milhão * 200 bytes ~ 200 MB  
  
     Índice não clusterizado A: 1 milhão * 50 bytes / 80% ~ 63 MB  
  
     Índice não clusterizado B: 1 milhão * 80 bytes / 80% ~ 100 MB  
  
     Tamanho total de estruturas existentes: 363 MB  
  
2.  Determine o tamanho das estruturas de índice de destino. Suponha que a nova chave clusterizada tenha 24 bytes de tamanho, incluindo um uniqueifier. O indicador de linha (8 bytes de comprimento) nos dois índices não clusterizados será substituído por esta chave clusterizada.  
  
     Índice clusterizado: 1 milhão * 200 bytes / 80% ~ 250 MB  
  
     Índice não clusterizado A: 1 milhão * (50 – 8 + 24) bytes / 80% ~ 83 MB  
  
     Índice não clusterizado B: 1 milhão * (80 – 8 + 24) bytes / 80% ~ 120 MB  
  
     Tamanho total de novas estruturas: 453 MB  
  
     Espaço em disco total exigido para aceitar ambas as estruturas de fonte e destino para a duração da operação de índice é de 816 MB (363 + 453). O espaço atualmente alocado às estruturas de fonte será desalocado depois que a operação de índice estiver confirmada.  
  
3.  Determine o espaço em disco temporário para classificação.  
  
     Os requisitos de espaço são exibidos para classificação em **tempdb** (com SORT_IN_TEMPDB definido como ON) e a classificação no local de destino (com SORT_IN_TEMPDB definido como OFF).  
  
    1.  Quando SORT_IN_TEMPDB estiver definido como ON, **tempdb** deverá ter espaço em disco suficiente para manter o maior índice (1 milhão * 200 bytes ~ 200 MB). O fator de preenchimento não é considerado na operação de classificação.  
  
         Espaço em disco adicional (no local do **tempdb** ) igual ao valor de [Configurar a opção index create memory de configuração de servidor](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) = 2 MB.  
  
         Tamanho total de espaço em disco temporário com SORT_IN_TEMPDB é definido como ON ~ 202 MB.  
  
    2.  Quando SORT_IN_TEMPDB é definido como OFF (padrão), os 250 MB de espaço de disco já considerados para o novo índice no passo 2 é usado para classificação.  
  
         Espaço em disco adicional (no local de destino) igual ao valor de [Configurar a opção index create memory de configuração de servidor](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) = 2 MB.  
  
         O tamanho total de espaço em disco temporário com SORT_IN_TEMPDB é definido como OFF = 2 MB.  
  
 Usando **tempdb**, um total de 1018 MB (816 + 202) seria necessário para criar os índices clusterizados e não clusterizados. Embora o uso do **tempdb** aumente o total de espaço em disco temporário usado para criar um índice, ele pode reduzir o tempo necessário para criar um índice quando **tempdb** estiver em um conjunto diferente de discos do que aqueles no banco de dados do usuário. Para obter mais informações sobre como usar o **tempdb**, veja [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 Sem usar o **tempdb**, um total de 818 MB (816+ 2) seriam necessários para criar índices clusterizados e não clusterizados.  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>Cálculos de espaço em disco para uma operação de índice online  
 Quando você cria, cancela ou recria um índice clusterizados online, é necessário espaço adicional em disco para criar e manter um índice de mapeamento temporário. Este índice de mapeamento temporário contém um registro para cada linha na tabela e seu conteúdo é a união das colunas de indicadores velhas e novas.  
  
 Para calcular o espaço em disco precisado para uma operação de índice clusterizado online, siga os passos mostrados para uma operação de índice offline, e acrescente esses resultados aos resultados do passo seguinte.  
  
-   Determine espaço para o índice de mapeamento temporário.  
  
     Neste exemplo, o indicador antigo é a fila ID (RID) do heap (8 bytes) e o novo indicador é a chave de clusterização (24 bytes incluindo um **uniqueifier**). Não há nenhuma coluna sobreposta entre os indicadores novos e velhos.  
  
     Tamanho de índice de mapeamento temporário = 1 milhão * (8 bytes + 24 bytes) / 80% ~ 40 MB.  
  
     Esse espaço em disco deve ser adicionado ao espaço em disco necessário no local de destino se SORT_IN_TEMPDB estiver definido como OFF, ou para **tempdb** se SORT_IN_TEMPDB estiver definido como ON.  
  
 Para obter mais informações sobre o índice de mapeamento temporário, veja [Requisitos de espaço em disco para operações de índice DDL](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="disk-space-summary"></a>Resumo de espaço em disco  
 A tabela a seguir resume os resultados dos cálculos de espaço em disco.  
  
|Operação de índice|Os requisitos de espaço em disco para os locais das seguintes estruturas|  
|---------------------|---------------------------------------------------------------------------|  
|Operação de índice offline com SORT_IN_TEMPDB = ON|Espaço total durante a operação: 1018 MB<br /><br /> - Tabela e índices existentes: 363 MB\*<br /><br /> -<br />                    **tempdb**: 202 MB*<br /><br /> -Novos índices: 453 MB<br /><br /> Espaço total necessário após a operação: 453 MB|  
|Operação de índice offline com SORT_IN_TEMPDB = OFF|Espaço total durante a operação: 816 MB<br /><br /> -Tabela e índices existentes: 363 MB*<br /><br /> -Novos índices: 453 MB<br /><br /> Espaço total necessário após a operação: 453 MB|  
|Operação de índice online com SORT_IN_TEMPDB = ON|Espaço total durante a operação: 1058 MB<br /><br /> - Tabela e índices existentes: 363 MB\*<br /><br /> -<br />                    **tempdb** (inclui índice de mapeamento): 242 MB*<br /><br /> -Novos índices: 453 MB<br /><br /> Espaço total necessário após a operação: 453 MB|  
|Operação de índice online com SORT_IN_TEMPDB = OFF|Espaço total durante a operação: 856 MB<br /><br /> -Tabela e índices existentes: 363 MB*<br /><br /> - Índice de mapeamento temporário: 40 MB\*<br /><br /> -Novos índices: 453 MB<br /><br /> Espaço total necessário após a operação: 453 MB|  
  
 * Este espaço é desalocado depois que a operação de índice estiver confirmada.  
  
 Este exemplo não considera qualquer espaço em disco temporário adicional necessário em **tempdb** para registros de versão criados por atualização de usuário simultâneos e exclui operações.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Espaço em disco de log de transações para operações de índice](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
  
