---
title: Processamento inteligente de consultas em bancos de dados Microsoft SQL | Microsoft Docs
description: Recursos de processamento inteligente de consulta para melhorar o desempenho da consulta no SQL Server e no Banco de Dados SQL do Azure.
ms.custom: ''
ms.date: 05/22/2018
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7786fd048f1698c90f379450b31e0bac3457706e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455759"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Processamento inteligente de consultas em bancos de dados SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

A família de recursos **Processamento de consulta inteligente** contém recursos de amplo impacto que melhoram o desempenho de cargas de trabalho existentes com esforço mínimo de implementação.   Isso inclui aprimoramentos de constructos preexistentes e também a introdução de métodos e funcionalidades adaptáveis.  

## <a name="adaptive-query-processing"></a>Processamento de consulta adaptável
Dentro da família de recursos de processamento inteligente de consultas está a família de recursos de processamento de consulta adaptável lançada no SQL Server 2017 e no Banco de Dados SQL do Azure, que adicionou novas funcionalidades gerais de processamento de consulta que adaptam estratégias de otimização às condições de tempo de execução da carga de trabalho do seu aplicativo:
- **Junções adaptáveis de modo de lote**. Esse recurso permite que seu plano mude dinamicamente para uma melhor estratégia de junção durante a execução usando um único plano armazenado em cache.
- **Comentários de concessão de memória do modo de lote**. Esse recurso recalcula a memória real necessária para uma consulta e, em seguida, atualiza o valor de concessão para o plano armazenado em cache, reduzindo concessões de memória excessivas que afetam a simultaneidade e corrigindo concessões de memória subestimadas que causam derramamentos de alto custo para o disco.
- **Execução Intercalada para MSTVFs (funções com valor de tabela de várias instruções)**. Com a execução intercalada, usamos as contagens de linhas real da função para tornar decisões de plano de consulta downstream mais embasadas. 

Para obter mais informações sobre o processamento de consulta adaptável, veja [Processamento de consulta adaptável em bancos de dados SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="see-also"></a>Confira também
[Central de desempenho do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Junções](../../relational-databases/performance/joins.md)    
[Demonstrando o Processamento de Consulta Adaptável](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
