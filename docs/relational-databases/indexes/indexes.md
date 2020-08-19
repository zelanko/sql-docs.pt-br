---
description: Índices
title: Índices | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b8487f821b698974744fdc18453a2a5c8285d889
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88408002"
---
# <a name="indexes"></a>Índices
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

## <a name="available-index-types"></a>Tipos de índice disponíveis
A tabela a seguir lista os tipos de índices disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece links para informações adicionais.  
  
|Tipo de índice|Descrição|Informações adicionais|  
|----------------|-----------------|----------------------------|  
|Hash|Com um índice de hash, os dados são acessados por meio de uma tabela de hash na memória. Os índices de hash consomem uma quantidade fixa de memória, que é uma função do número de buckets.|[Diretrizes para usar índices em tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [Diretrizes de design de índice de hash](../../relational-databases/sql-server-index-design-guide.md#hash_index)|  
|Não clusterizado com otimização de memória|Para índices não clusterizados com otimização de memória, o consumo de memória é uma função da contagem de linhas e do tamanho das colunas de chave de índice.|[Diretrizes para usar índices em tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [Diretrizes de design de índice não clusterizado com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)|  
|Clusterizado|O índice clusterizado classifica e armazena as linhas de dados da tabela ou exibição em uma ordem com base na chave do índice clusterizado. O índice clusterizado é implementado como uma estrutura de índice da árvore B que oferece suporte à recuperação rápida de linhas com base em seus valores da chave de índice clusterizado.|[Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Criar índices clusterizados](../../relational-databases/indexes/create-clustered-indexes.md)<br /><br /> [Diretrizes de design de índice clusterizado](../../relational-databases/sql-server-index-design-guide.md#Clustered)|  
|Não clusterizado|Um índice não clusterizado pode ser definido em uma tabela ou exibição com um índice clusterizado ou em um heap. Cada linha do índice não clusterizado contém o valor da chave não clusterizada e um localizador de linha. Esse localizador aponta para a linha de dados no índice clusterizado ou heap que possui o valor da chave. As linhas do índice são armazenadas na ordem dos valores da chave de índice, mas não há garantias de que as linhas de dados estejam em uma determinada ordem, a menos que um índice clusterizado seja criado na tabela.|[Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Criar índices não clusterizados](../../relational-databases/indexes/create-nonclustered-indexes.md)<br /><br /> [Diretrizes de design de índice não clusterizado](../../relational-databases/sql-server-index-design-guide.md#Nonclustered)|  
|Exclusivo|Um índice exclusivo garante que a chave de índice não contenha valores duplicados; portanto, cada linha em uma tabela ou exibição é, de alguma forma, exclusiva.<br /><br /> A exclusividade pode ser uma propriedade de índices clusterizados e não clusterizados.|[Criar índices exclusivos](../../relational-databases/indexes/create-unique-indexes.md)<br /><br /> [Diretrizes de design de índice exclusivo](../../relational-databases/sql-server-index-design-guide.md#Unique)|  
|columnstore|Um índice columnstore na memória armazena e gerencia dados usando o armazenamento de dados baseado em coluna e o processamento de consulta baseado em coluna.<br /><br /> Os índices columnstore funcionam bem para as cargas de trabalho de data warehouse que executam principalmente carregamentos em massa e consultas somente leitura. Use o índice columnstore para obter um ganho de **desempenho de consulta até 10 vezes maior** sobre o armazenamento tradicional orientado por linha e de **compactação de dados até 7 vezes maior** sobre o tamanho dos dados não compactados.|[Guia de Índices columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)<br /><br /> [Diretrizes de design de índice columnstore](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)|  
|Índice com colunas incluídas|Um índice não clusterizado que é estendido para incluir colunas que não são de chave, além das colunas de chave.|[Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md)|  
|Índice em colunas computadas.|Um índice em uma coluna que é derivada do valor de uma ou mais colunas ou certas entradas deterministas.|[Índices em colunas computadas](../../relational-databases/indexes/indexes-on-computed-columns.md)|  
|Filtered|Um índice não clusterizado aperfeiçoado, especialmente indicado para abranger consultas que selecionam de um subconjunto bem definido de dados. Ele usa um predicado de filtro para indexar uma parte das linhas da tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta e reduzir os custos de manutenção e armazenamento do índice em comparação com os índices de tabela completa.|[Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md)<br /><br /> [Diretrizes de design de índice filtrado](../../relational-databases/sql-server-index-design-guide.md#Filtered)|  
|Espacial|Um índice espacial permite a execução de determinadas operações de forma mais eficiente em objetos espaciais (*dados espaciais*) em uma coluna do tipo de dados **geometry** . O índice espacial reduz o número de objetos nos quais operações espaciais relativamente dispendiosas precisam ser aplicadas.|[Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)|  
|XML|Uma representação fragmentada e persistente de BLOBS (objetos binários grandes) XML na coluna de tipo de dados **xml**.|[Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)|  
|Texto completo|Um tipo especial de índice funcional com base em token que é criado e mantido pelo Mecanismo de Texto Completo da Microsoft para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele fornece suporte eficiente para pesquisas sofisticadas de palavras em dados de cadeias de caracteres.|[Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md)      
 [Opção SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)     
 [Desabilitar índices e restrições](../../relational-databases/indexes/disable-indexes-and-constraints.md)     
 [Habilitar índices e restrições](../../relational-databases/indexes/enable-indexes-and-constraints.md)    
 [Renomear índices](../../relational-databases/indexes/rename-indexes.md)     
 [Opções Set Index](../../relational-databases/indexes/set-index-options.md)     
 [Requisitos de espaço em disco para operações de DDL de índice](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)     
 [Reorganizar e recompilar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)     
 [Especificar o fator de preenchimento para um índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)     
 [Guia de arquitetura de página e extensões](../../relational-databases/pages-and-extents-architecture-guide.md)     
 [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
