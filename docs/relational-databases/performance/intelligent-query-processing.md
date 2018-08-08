---
title: Processamento inteligente de consultas em bancos de dados Microsoft SQL | Microsoft Docs
description: Recursos de processamento inteligente de consulta para melhorar o desempenho da consulta no SQL Server e no Banco de Dados SQL do Azure.
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 20c453617ccef36166ca3b9fae62ee0430959e51
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562950"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Processamento inteligente de consultas em bancos de dados SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

A família de recursos **Processamento de consulta inteligente** inclui recursos de amplo impacto que melhoram o desempenho de cargas de trabalho existentes com esforço mínimo de implementação.

![Recursos de processamento de consulta inteligente](./media/1_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>Processamento de consulta adaptável
A família de recursos de processamento de consulta adaptável inclui aprimoramentos do processo de consulta que adaptará estratégias de otimização para as condições de tempo de execução da carga de trabalho do aplicativo. Esses aprimoramentos incluem: uniões adaptáveis do modo de lote, comentários de concessão de memória e execução intercalada para funções com valor de tabela e várias instruções.

### <a name="batch-mode-adaptive-joins"></a>Junções adaptáveis de modo de lote
Esse recurso permite que seu plano mude dinamicamente para uma melhor estratégia de junção durante a execução usando um único plano armazenado em cache.

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Comentários de concessão de memória do modo de lote e linha
Esse recurso recalcula a memória real necessária para uma consulta e, em seguida, atualiza o valor de concessão para o plano armazenado em cache, reduzindo concessões de memória excessivas que afetam a simultaneidade e corrigindo concessões de memória subestimadas que causam derramamentos de alto custo para o disco.

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>Execução Intercalada para MSTVFs (funções com valor de tabela de várias instruções)
Com a execução intercalada, as contagens de linha reais da função são usadas para tornar decisões de plano de consulta downstream mais embasadas. 

Para saber mais, confira [Processamento de consultas adaptável em bancos de dados SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilação adiada de variável da tabela
A compilação adiada de variável da tabela melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e compilação inicial, esse recurso propagará estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela.  Essas informações de contagem de linha precisas serão ser usadas para otimizar operações de plano de downstream.

Com a compilação adiada de variável de tabela, a compilação de uma instrução que faz referência a uma variável de tabela é adiada até a primeira execução real da instrução. Esse comportamento de compilação adiada é idêntico ao comportamento das tabelas temporárias, e essa alteração resulta no uso de cardinalidade real, em vez do palpite original de uma linha. Para habilitar a versão prévia da compilação adiada de variável de tabela no Banco de Dados SQL do Azure, habilite o nível de compatibilidade do banco de dados 150 para o banco de dados ao qual você está conectado ao executar a consulta.

Para saber mais, veja [Compilação adiada de variável da tabela](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="approximate-query-processing"></a>Processamento de consulta aproximada
O processamento de consulta aproximada é uma nova família de recursos projetados para fornecer agregações em grandes conjuntos de dados, nos quais a capacidade de resposta é mais importante do que a precisão absoluta.  Um exemplo pode ser o cálculo de um COUNT(DISTINCT()) entre 10 bilhões de linhas, para exibição em um painel.  Nesse caso, a precisão absoluto não é importante, mas a capacidade de resposta é essencial. A nova função de agregação APPROX_COUNT_DISTINCT retorna o número aproximado de valores não nulos exclusivos em um grupo.

Para saber mais, confira [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="see-also"></a>Confira também
[Central de desempenho do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Junções](../../relational-databases/performance/joins.md)    
[Demonstrando o Processamento de Consulta Adaptável](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
