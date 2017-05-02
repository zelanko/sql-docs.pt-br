---
title: "Índices | Microsoft Docs"
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2f4ac3c815fec2e6add64257dd2ae12e7b659f84
ms.lasthandoff: 04/11/2017

---
# <a name="indexes"></a>Índices
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  A tabela a seguir lista os tipos de índices disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece links para informações adicionais.  
  
|Tipo de índice|Descrição|Informações adicionais|  
|----------------|-----------------|----------------------------|  
|Hash|Com um índice de hash, os dados são acessados por meio de uma tabela de hash na memória. Os índices de hash consomem uma quantidade fixa de memória, que é uma função do número de buckets.|[Diretrizes para usar índices em tabelas com otimização de memória](http://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)|  
|índices não clusterizados com otimização de memória|Para índices não clusterizados com otimização de memória, o consumo de memória é uma função da contagem de linhas e do tamanho das colunas de chave de índice.|[Diretrizes para usar índices em tabelas com otimização de memória](http://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)|  
|Clusterizado|O índice clusterizado classifica e armazena as linhas de dados da tabela ou exibição em uma ordem com base na chave do índice clusterizado. O índice clusterizado é implementado como uma estrutura de índice da árvore B que oferece suporte à recuperação rápida de linhas com base em seus valores da chave de índice clusterizado.|[Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md)|  
|Não clusterizado|Um índice não clusterizado pode ser definido em uma tabela ou exibição com um índice clusterizado ou em um heap. Cada linha do índice não clusterizado contém o valor da chave não clusterizada e um localizador de linha. Esse localizador aponta para a linha de dados no índice clusterizado ou heap que possui o valor da chave. As linhas do índice são armazenadas na ordem dos valores da chave de índice, mas não há garantias de que as linhas de dados estejam em uma determinada ordem, a menos que um índice clusterizado seja criado na tabela.|[Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Criar índices não clusterizados](../../relational-databases/indexes/create-nonclustered-indexes.md)|  
|Exclusivo|Um índice exclusivo garante que a chave de índice não contenha valores duplicados; portanto, cada linha em uma tabela ou exibição é, de alguma forma, exclusiva.<br /><br /> A exclusividade pode ser uma propriedade de índices clusterizados e não clusterizados.|[Criar índices exclusivos](../../relational-databases/indexes/create-unique-indexes.md)|  
|columnstore|Um índice columnstore na memória armazena e gerencia dados usando o armazenamento de dados baseado em coluna e o processamento de consulta baseado em coluna.<br /><br /> Os índices columnstore funcionam bem para as cargas de trabalho de data warehouse que executam principalmente carregamentos em massa e consultas somente leitura. Use o índice columnstore para obter um ganho de **desempenho de consulta até 10 vezes maior** sobre o armazenamento tradicional orientado por linha e de **compactação de dados até 7 vezes maior** sobre o tamanho dos dados não compactados.|[Guia de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)<br /><br /> [Usando índices Columnstore não clusterizados](https://msdn.microsoft.com/library/dn589806.aspx)|  
|Índice com colunas incluídas|Um índice não clusterizado que é estendido para incluir colunas que não são de chave, além das colunas de chave.|[Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md)|  
|Índice em colunas computadas.|Um índice em uma coluna que é derivada do valor de uma ou mais colunas ou certas entradas deterministas.|[Índices em colunas computadas](../../relational-databases/indexes/indexes-on-computed-columns.md)|  
|Filtrado|Um índice não clusterizado aperfeiçoado, especialmente indicado para abranger consultas que selecionam de um subconjunto bem definido de dados. Ele usa um predicado de filtro para indexar uma parte das linhas da tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta e reduzir os custos de manutenção e armazenamento do índice em comparação com os índices de tabela completa.|[Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md)|  
|Espacial|Um índice espacial permite a execução de determinadas operações de forma mais eficiente em objetos espaciais (*dados espaciais*) em uma coluna do tipo de dados **geometry** . O índice espacial reduz o número de objetos nos quais operações espaciais relativamente dispendiosas precisam ser aplicadas.|[Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)|  
|XML|Uma representação fragmentada e persistente de BLOBS (objetos binários grandes) XML na coluna de tipo de dados **xml**.|[Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)|  
|Texto completo|Um tipo especial de índice funcional com base em token que é criado e mantido pelo Mecanismo de Texto Completo da Microsoft para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele fornece suporte eficiente para pesquisas sofisticadas de palavras em dados de cadeias de caracteres.|[Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
  
 [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md)  
  
 [Habilitar índices e restrições](../../relational-databases/indexes/enable-indexes-and-constraints.md)  
  
 [Renomear índices](../../relational-databases/indexes/rename-indexes.md)  
  
 [Definir opções de índice](../../relational-databases/indexes/set-index-options.md)  
  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
 [Especificar fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  

[Guia de arquitetura de página e extensões](../../relational-databases/pages-and-extents-architecture-guide.md)
  
## <a name="see-also"></a>Consulte também  
 [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)  
  
  

