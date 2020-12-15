---
title: Subexpressão comum
description: Exibe o exemplo de melhoria de consulta que foi introduzido no Analytics Platform System CU 7.3
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7'
ms.openlocfilehash: 8dfadabcae27ff8705d86294b1c05851245d199c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97420195"
---
# <a name="common-subexpression-elimination-explained"></a>Eliminação de subexpressão comum explicada

O APS CU 7.3 melhora o desempenho da consulta com a eliminação de subexpressão comum no otimizador de consulta do SQL. A melhoria melhora as consultas de duas maneiras. O primeiro benefício é a capacidade de identificar e eliminar essas expressões, ajudando a reduzir o tempo de compilação do SQL. O segundo e mais importante benefício é que as operações de movimentação de dados para essas subexpressões redundantes são eliminadas, portanto, o tempo de execução das consultas se torna mais rápido.

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
Considere a consulta acima das ferramentas de benchmark do TPC-DS.  Na consulta acima, a subconsulta é a mesma, mas a cláusula order by com Rank () sobre a função é classificada de duas maneiras diferentes. Anterior à CU 7.3, essa subconsulta será avaliada e executada duas vezes, uma para ordem crescente e uma vez para ordem decrescente, incorrendo duas operações de movimentação de dados. Depois de instalar o APS CU 7.3, a parte da subconsulta será avaliada uma vez, reduzindo a movimentação de dados e finalizando a consulta mais rapidamente.

Apresentamos uma [opção de recurso](appliance-feature-switch.md) chamada ' OptimizeCommonSubExpressions ' que permitirá que você teste o recurso mesmo depois de atualizar para o APS cu 7.3. O recurso está ativado por padrão, mas pode ser desativado. 

> [!NOTE] 
> As alterações nos valores de switch de recursos exigem uma reinicialização do serviço.

Você pode experimentar a consulta de exemplo criando as tabelas a seguir em seu ambiente de teste e avaliando o plano de explicação para a consulta mencionada acima. 

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
Se você examinar o plano de explicação da consulta, verá que antes da CU 7.3 (ou quando a opção do recurso estiver desativada), a consulta terá 17 número total de operações e, depois da CU 7.3 (ou com a opção de recurso ativada) a mesma consulta mostrará 9 número total de operações. Se você apenas contar as operações de movimentação de dados, verá que o plano anterior tem quatro operações de movimentação versus duas operações de movimentação no novo plano. O novo otimizador de consulta foi capaz de reduzir duas operações de movimentação de dados reutilizando a tabela temporária já criada com o novo plano, reduzindo o tempo de execução de consulta. 


