---
title: Requisitos de espaço em disco para operações de índice DDL | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e49ef1ad379f675ca457f8cd9c82a5e4ecc3fd04
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68107132"
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>Disk Space Requirements for Index DDL Operations
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O espaço em disco é uma consideração importante ao criar, recriar ou cancelar índices. Um espaço em disco inadequado pode degradar o desempenho ou até mesmo provocar falha na operação de índice. Este tópico fornece informações gerais que poderão lhe ajudar a determinar a quantidade de espaço em disco necessária para operações DDL (Linguagem de Definição de Dados) de índice.  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>Operações de índice que não requerem espaço adicional em disco  
 As operações de índice que não requerem nenhum espaço adicional em disco são:  
  
-   ALTER INDEX REORGANIZE; porém, espaço de log é necessário.  
  
-   DROP INDEX, quando se está cancelando um índice não clusterizado.  
  
-   DROP INDEX quando se está cancelando um índice clusterizado offline sem especificar a cláusula MOVE TO e quando não houver índices não clusterizados.  
  
-   CREATE TABLE (restrições PRIMARY KEY ou UNIQUE)  
  
## <a name="index-operations-that-require-additional-disk-space"></a>Operações de índice que requerem espaço adicional em disco  
 Todas as outras operações de índice DDL exigem espaço adicional temporário em disco para serem utilizadas na operação, e espaço permanente em disco para armazenar a nova estrutura ou estruturas de índice.  
  
 Quando uma nova estrutura de índice é criada, o espaço em disco de ambas as estruturas, a antiga (origem) e a nova (destino), é necessário para os arquivos e grupos de arquivos apropriados. A estrutura antiga não é desalocada até que a transação de criação do índice seja confirmada.  
  
 As seguintes operações de índice DDL criam novas estruturas de índice e exigem espaço adicional em disco:  
  
-   CREATE INDEX  
  
-   CREATE INDEX WITH DROP_EXISTING  
  
-   ALTER INDEX REBUILD  
  
-   ALTER TABLE ADD CONSTRAINT (PRIMARY KEY ou UNIQUE)  
  
-   ALTER TABLE DROP CONSTRAINT (PRIMARY KEY ou UNIQUE) quando a restrição tem base em um índice clusterizado  
  
-   DROP INDEX MOVE TO (Aplica-se somente a índices clusterizados.)  
  
## <a name="temporary-disk-space-for-sorting"></a>Espaço em disco temporário para classificação  
 Além do espaço em disco exigido para as estruturas de origem e destino, o espaço em disco temporário é necessário para classificar, a menos que o otimizador de consulta localize um plano de execução que não exija classificação.  
  
 Quando a classificação for necessária, a classificação será de um índice novo por vez. Por exemplo, quando você recria um índice clusterizado e índices não clusterizados associados dentro de uma única instrução, os índices são classificados um após o outro. Portanto, o espaço em disco temporário adicional, exigido apenas para classificar, terá que ser tão grande quanto o maior índice da operação. Esse, quase sempre, é o índice clusterizado.  
  
 Se a opção SORT_IN_TEMPDB for definida como ON, o maior índice deverá se ajustar à **tempdb**. Embora essa opção aumente a quantidade de espaço temporário em disco que é usado para criar um índice, pode reduzir o tempo necessário à criação de um índice quando **tempdb** estiver em um conjunto de discos diverso do banco de dados de usuário.  
  
 Se SORT_IN_TEMPDB for definida como OFF (padrão), todos os índices, inclusive os índices particionados, serão classificados em seu espaço de disco de destino. Apenas o espaço em disco das estruturas do novo índice será requerido.  
  
 Para obter um exemplo de cálculo de espaço em disco, consulte [Index Disk Space Example](../../relational-databases/indexes/index-disk-space-example.md).  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>Espaço temporário em disco para operações de índice online  
 Quando se executam operações de índice online é necessário espaço temporário adicional em disco.  
  
 Se um índice clusterizado for criado, recriado, ou cancelado online, um índice não clusterizado temporário será criado para mapear indicadores antigos para os indicadores novos. Se a opção SORT_IN_TEMPDB for definida como ON, esse índice temporário será criado em **tempdb**. Se SORT_IN_TEMPDB for definida como OFF, o mesmo grupo de arquivos ou esquema de partição do índice de destino serão usados. O índice temporário de mapeamento contém um registro para cada linha da tabela, e seus conteúdos são a união das colunas de indicadores antigas e novas, incluindo indicadores de exclusividade, mais identificadores de registro e incluindo apenas uma cópia única de todas as colunas usadas em ambos os indicadores. Para obter mais informações sobre operações de índice online, consulte [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
> [!NOTE]  
>  A opção SORT_IN_TEMPDB não pode ser definida para instruções DROP INDEX. O índice temporário de mapeamento é sempre criado no mesmo grupo de arquivos ou esquema de partição que o índice de destino.  
  
 As operações de índice online utilizam o controle de versão de linha para isolar a operação de índice dos efeitos das modificações feitas por outras transações. Isso evita a necessidade de solicitar bloqueios de compartilhamento de linhas já lidas. As operações simultâneas de atualização e exclusão de usuários durante operações de índice online precisam de espaço para os registros de versão no **tempdb**. Para obter mais informações, consulte [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md) .  
  
## <a name="related-tasks"></a>Related Tasks  
 [Exemplo de espaço em disco de índice](../../relational-databases/indexes/index-disk-space-example.md)  
  
 [Espaço em disco de log de transações para operações de índice](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
 [Estimar o tamanho de uma tabela](../../relational-databases/databases/estimate-the-size-of-a-table.md)  
  
 [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)  
  
 [Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [Estimar o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [Especificar o fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
 [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
  
