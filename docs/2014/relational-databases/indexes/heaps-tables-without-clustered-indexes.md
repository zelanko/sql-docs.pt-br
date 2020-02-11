---
title: Heaps (tabelas sem índices clusterizados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de71808c54264639aea82fe66cf23a7bfd6bd0ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63162157"
---
# <a name="heaps-tables-without-clustered-indexes"></a>Heaps (Tabelas sem índices clusterizados)
  Heap é uma tabela sem índice clusterizado. Podem ser criados um ou mais índices não clusterizados em tabelas armazenadas como um heap. Dados são armazenados no heap sem especificar uma ordem. Normalmente, os dados são armazenados inicialmente na ordem em que as linhas são inseridas na tabela, mas o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode mover os dados no heap para armazenar as linhas de forma eficaz; portanto, a ordem de dados não pode ser prevista. Para garantir a ordem de linhas retornadas de um heap, você deve usar a cláusula `ORDER BY`. Para especificar a ordem de armazenamento das linhas, crie um índice clusterizado na tabela, de forma que a tabela não seja um heap.  
  
> [!NOTE]  
>  Às vezes, há boas razões para deixar uma tabela como heap em vez de criar um índice clusterizado, mas usar heaps efetivamente é uma habilidade avançada. A maioria das tabelas deve ter um índice clusterizado cuidadosamente escolhido, a menos que haja uma boa razão boa para deixar a tabela como heap.  
  
## <a name="when-to-use-a-heap"></a>Quando usar um heap  
 Se uma tabela for um heap e não tiver um índice clusterizado, a tabela inteira deverá ser examinada (análise de tabela) para localizar as linhas. Isso pode ser aceitável quando a tabela é pequena, como uma lista dos 12 escritórios regionais de uma empresa.  
  
 Quando uma tabela é armazenada como heap, linhas individuais são identificadas por referência a um RID (identificador de linha) que consiste em número do arquivo, número da página de dados e local na página. A ID de linha é uma estrutura pequena e eficiente. Às vezes, os arquitetos de dados usam heaps quando os dados são sempre acessados por índices não clusterizados e o RID é menor que uma chave de índice clusterizado.  
  
## <a name="when-not-to-use-a-heap"></a>Quando não usar um heap  
 Não use um heap quando os dados são retornados frequentemente em uma ordem classificada. Um índice clusterizado na coluna de classificação pode evitar a operação de classificação.  
  
 Não use um heap quando os dados forem agrupados com frequência. Os dados devem ser classificados antes de serem agrupados, e um índice clusterizado na coluna de classificação pode evitar a operação de classificação.  
  
 Não use um heap quando intervalos de dados são consultados frequentemente na tabela.  Um índice clusterizado na coluna de intervalo pode evitar a classificação do heap inteiro.  
  
 Não use um heap quando não houver índice não clusterizado e a tabela for grande. Em um heap, todas as linhas do heap devem ser lidas para localizar qualquer linha.  
  
## <a name="managing-heaps"></a>Gerenciando heaps  
 Para criar um heap, crie uma tabela sem um índice clusterizado. Se uma tabela já tiver um índice clusterizado, descarte o índice clusterizado para retornar a tabela a um heap.  
  
 Para remover um heap, crie um índice clusterizado no heap.  
  
 Para recriar um heap para recuperar o espaço desperdiçado, crie um índice clusterizado no heap e descarte esse índice clusterizado.  
  
> [!WARNING]  
>  Criar ou descartar índices clusterizados requer a regravação da tabela inteira. Se a tabela tiver índices não clusterizados, todos os índices não clusterizados deverão ser recriados sempre que o índice clusterizado for alterado. Portanto, mudar de um heap para uma estrutura de índice clusterizado ou vice-versa pode demorar muito e exigir espaço em disco para reorganizar os dados em tempdb.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [Índices clusterizados e não clusterizados descritos](clustered-and-nonclustered-indexes-described.md)  
  
  
