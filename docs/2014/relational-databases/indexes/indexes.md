---
title: Índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: be474ea547222c30321d893ee8a1ce6f0af0be39
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049883"
---
# <a name="indexes"></a>Índices
  A tabela a seguir lista os tipos de índices disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece links para informações adicionais.  
  
|Tipo de índice|Descrição|Informações adicionais|  
|----------------|-----------------|----------------------------|  
|Hash|Com um índice de hash, os dados são acessados por meio de uma tabela de hash na memória. Os índices de hash consomem uma quantidade fixa de memória, que é uma função do número de buckets.|[Diretrizes para usar índices em tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md)|  
|índices não clusterizados com otimização de memória|Para índices não clusterizados com otimização de memória, o consumo de memória é uma função da contagem de linhas e do tamanho das colunas de chave de índice.|[Diretrizes para usar índices em tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md)|  
|Clusterizado|O índice clusterizado classifica e armazena as linhas de dados da tabela ou exibição em uma ordem com base na chave do índice clusterizado. O índice clusterizado é implementado como uma estrutura de índice da árvore B que oferece suporte à recuperação rápida de linhas com base em seus valores da chave de índice clusterizado.|[Índices clusterizados e não clusterizados descritos](clustered-and-nonclustered-indexes-described.md)<br /><br /> [Criar índices clusterizados](create-clustered-indexes.md)|  
|Não clusterizado|Um índice não clusterizado pode ser definido em uma tabela ou exibição com um índice clusterizado ou em um heap. Cada linha do índice não clusterizado contém o valor da chave não clusterizada e um localizador de linha. Esse localizador aponta para a linha de dados no índice clusterizado ou heap que possui o valor da chave. As linhas do índice são armazenadas na ordem dos valores da chave de índice, mas não há garantias de que as linhas de dados estejam em uma determinada ordem, a menos que um índice clusterizado seja criado na tabela.|[Índices clusterizados e não clusterizados descritos](clustered-and-nonclustered-indexes-described.md)<br /><br /> [Criar índices não clusterizados](create-nonclustered-indexes.md)|  
|Exclusivo|Um índice exclusivo garante que a chave de índice não contenha valores duplicados; portanto, cada linha em uma tabela ou exibição é, de alguma forma, exclusiva.<br /><br /> A exclusividade pode ser uma propriedade de índices clusterizados e não clusterizados.|[Criar índices exclusivos](create-unique-indexes.md)|  
|columnstore|Um índice columnstore na memória armazena e gerencia dados usando o armazenamento de dados baseado em coluna e o processamento de consulta baseado em coluna.<br /><br /> Os índices columnstore funcionam bem para as cargas de trabalho de data warehouse que executam principalmente carregamentos em massa e consultas somente leitura. Use o índice columnstore para obter um ganho de **desempenho de consulta até 10 vezes maior** sobre o armazenamento tradicional orientado por linha e de **compactação de dados até 7 vezes maior** sobre o tamanho dos dados não compactados.|[Columnstore Indexes Described](columnstore-indexes-described.md)<br /><br /> [Usando índices Columnstore não clusterizados](../../database-engine/using-nonclustered-columnstore-indexes.md)<br /><br /> [Usando índices columnstore clusterizados](../../database-engine/using-clustered-columnstore-indexes.md)|  
|Índice com colunas incluídas|Um índice não clusterizado que é estendido para incluir colunas que não são de chave, além das colunas de chave.|[Criar índices com colunas incluídas](create-indexes-with-included-columns.md)|  
|Índice em colunas computadas.|Um índice em uma coluna que é derivada do valor de uma ou mais colunas ou certas entradas deterministas.|[Índices em colunas computadas](indexes-on-computed-columns.md)|  
|Filtered|Um índice não clusterizado aperfeiçoado, especialmente indicado para abranger consultas que selecionam de um subconjunto bem definido de dados. Ele usa um predicado de filtro para indexar uma parte das linhas da tabela. Um índice filtrado bem projetado pode melhorar o desempenho da consulta e reduzir os custos de manutenção e armazenamento do índice em comparação com os índices de tabela completa.|[Criar índices filtrados](create-filtered-indexes.md)|  
|Espacial|Um índice espacial permite a execução de determinadas operações de forma mais eficiente em objetos espaciais (*dados espaciais*) em uma coluna do tipo de dados **geometry** . O índice espacial reduz o número de objetos nos quais operações espaciais relativamente dispendiosas precisam ser aplicadas.|[Visão geral de índices espaciais](../spatial/spatial-indexes-overview.md)|  
|XML|Uma representação fragmentada e persistente de BLOBS (objetos binários grandes) XML na coluna de tipo de dados `xml`.|[Índices XML &#40;SQL Server&#41;](../xml/xml-indexes-sql-server.md)|  
|Texto completo|Um tipo especial de índice funcional com base em token que é criado e mantido pelo Mecanismo de Texto Completo da Microsoft para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele fornece suporte eficiente para pesquisas sofisticadas de palavras em dados de cadeias de caracteres.|[Popular índices de texto completo](../search/populate-full-text-indexes.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Opção SORT_IN_TEMPDB para índices](sort-in-tempdb-option-for-indexes.md)  
  
 [Desabilitar índices e restrições](disable-indexes-and-constraints.md)  
  
 [Habilitar índices e restrições](enable-indexes-and-constraints.md)  
  
 [Renomear índices](rename-indexes.md)  
  
 [Definir opções de índice](set-index-options.md)  
  
 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)  
  
 [Reorganizar e recompilar índices](reorganize-and-rebuild-indexes.md)  
  
 [Especificar fator de preenchimento para um índice](specify-fill-factor-for-an-index.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Índices clusterizados e não clusterizados descritos](clustered-and-nonclustered-indexes-described.md)  
  
  
