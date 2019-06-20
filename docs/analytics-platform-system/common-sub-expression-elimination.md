---
title: Subexpressão comum é explicado no Analytics Platform System | Microsoft Docs
description: Exibe o aperfeiçoamento de consulta de exemplo que foi introduzido no Analytics Platform System CU7.3
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 2dd02bed55f3d3781428eae3ec4bc2d0655819ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312467"
---
# <a name="common-subexpression-elimination-explained"></a>Eliminação de subexpressão comum explicada

APS CU7.3 melhora o desempenho de consulta com eliminação de subexpressão comum no otimizador de consulta SQL. O aprimoramento melhora a consultas de duas maneiras. A primeira vantagem é a capacidade de identificar e eliminar tais expressões ajudam a reduzir o tempo de compilação do SQL. O benefício de segundo e mais importante é que operações de movimentação de dados para essas subexpressão com redundância são eliminadas, portanto, o tempo de execução para consultas se torna mais rápido.

```sql
select top 100 asceding.rnk, i1.i_product_name best_performing, i2.i_product_name worst_performing
  from(select *
       from (select item_sk,rank() over (order by rank_col asc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V1)V11
       where rnk  < 11) asceding,
      (select *
       from (select item_sk,rank() over (order by rank_col desc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V2)V21
       where rnk  < 11) descending,
  item i1,
  item i2
  where asceding.rnk = descending.rnk
    and i1.i_item_sk=asceding.item_sk
    and i2.i_item_sk=descending.item_sk
  order by asceding.rnk
  ;
```
Considere a consulta acima das ferramentas de benchmark TPC-DS.  Na consulta anterior, a subconsulta é o mesmo, mas a cláusula order by com Rank pela função é classificada em duas maneiras diferentes. Anteriores ao CU7.3, essa subconsulta será obter avaliada e executada duas vezes, uma vez para ordem crescente e uma vez para ordem decrescente, incorrendo em duas operações de movimentação de dados. Depois de instalar CU7.3 APS, a parte de subconsulta será avaliada uma vez, portanto, reduzindo a movimentação de dados e concluir a consulta mais rápida.

Apresentamos uma [comutador de recurso](appliance-feature-switch.md) chamado 'OptimizeCommonSubExpressions' que permitirá a você testar o recurso, até mesmo após a atualização para CU7.3 APS. O recurso é ativado por padrão, mas pode ser desativado. 

> [!NOTE] 
> Alterações em valores de switch de recursos exigem uma reinicialização do serviço.

Você pode tentar a consulta de exemplo criando as tabelas a seguir em seu ambiente de teste e avaliando o plano de explicar para a consulta mencionado acima. 

```sql
CREATE TABLE [dbo].[store_sales] (
    [ss_sold_date_sk] int NULL, 
    [ss_sold_time_sk] int NULL, 
    [ss_item_sk] int NOT NULL, 
    [ss_customer_sk] int NULL, 
    [ss_cdemo_sk] int NULL, 
    [ss_hdemo_sk] int NULL, 
    [ss_addr_sk] int NULL, 
    [ss_store_sk] int NULL, 
    [ss_promo_sk] int NULL, 
    [ss_ticket_number] int NOT NULL, 
    [ss_quantity] int NULL, 
    [ss_wholesale_cost] decimal(7, 2) NULL, 
    [ss_list_price] decimal(7, 2) NULL, 
    [ss_sales_price] decimal(7, 2) NULL, 
    [ss_ext_discount_amt] decimal(7, 2) NULL, 
    [ss_ext_sales_price] decimal(7, 2) NULL, 
    [ss_ext_wholesale_cost] decimal(7, 2) NULL, 
    [ss_ext_list_price] decimal(7, 2) NULL, 
    [ss_ext_tax] decimal(7, 2) NULL, 
    [ss_coupon_amt] decimal(7, 2) NULL, 
    [ss_net_paid] decimal(7, 2) NULL, 
    [ss_net_paid_inc_tax] decimal(7, 2) NULL, 
    [ss_net_profit] decimal(7, 2) NULL
)
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([ss_item_sk]),  PARTITION ([ss_sold_date_sk] RANGE RIGHT FOR VALUES (2450815, 2451180, 2451545, 2451911, 2452276, 2452641, 2453006)));

CREATE TABLE [dbo].[item] (
    [i_item_sk] int NOT NULL, 
    [i_item_id] char(16) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, 
    [i_rec_start_date] date NULL, 
    [i_rec_end_date] date NULL, 
    [i_item_desc] varchar(200) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_current_price] decimal(7, 2) NULL, 
    [i_wholesale_cost] decimal(7, 2) NULL, 
    [i_brand_id] int NULL, 
    [i_brand] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_class_id] int NULL, 
    [i_class] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_category_id] int NULL, 
    [i_category] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manufact_id] int NULL, 
    [i_manufact] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_size] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_formulation] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_color] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_units] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_container] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manager_id] int NULL, 
    [i_product_name] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL
)
WITH (CLUSTERED INDEX ( [i_item_sk] ASC ), DISTRIBUTION = REPLICATE);
```
Se você examinar o plano de explicar da consulta, você verá que antes CU7.3 (ou quando a opção de recurso está desativado) a consulta tem 17 número total de operações e depois CU7.3 (ou com a opção de recurso ativado) a mesma consulta mostra 9 o número total de operações. Se você contar apenas as operações de movimentação de dados, você verá que o plano anterior tem quatro operações de movimentação versus duas operações de movimentação no novo plano. O novo Otimizador de consulta não conseguiu reduzir duas operações de movimentação de dados com a reutilização da tabela temporária que ele já criado com o novo plano, reduzindo o tempo de execução de consulta. 


