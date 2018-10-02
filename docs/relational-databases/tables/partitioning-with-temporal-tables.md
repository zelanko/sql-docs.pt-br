---
title: Particionamento com tabelas temporais | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 604e085a85a53730df94f436030ea0a0b31cf691
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784894"
---
# <a name="partitioning-with-temporal-tables"></a>Particionamento de Tabelas Temporais
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode usar o particionamento na tabela atual e de histórico de forma independente. No entanto, o particionamento não pode ser usado para alterar o conteúdo dos dados sem o controle da versão do sistema.  
  
> [!NOTE]  
>  O particionamento é um recurso do Enterprise Edition no SQL Server 2016 antes do Service Pack 1 e versões anteriores. Há suporte para particionamento em todas as edições no SQL Server 2016 Service Pack 1 e versões posteriores.
  
-   **Tabela atual:**  
  
    -   **SWITCH IN** na tabela atual para facilitar o carregamento de dados e a consulta enquanto o **SYSTEM_VERSIONING** estiver **ON**  
  
    -   **SWITCH OUT** não é permitido enquanto **SYSTEM_VERSIONING** estiver **ON**  
  
-   **Tabela de histórico:**  
  
    -   É possível executar o**SWITCH OUT** na tabela de hestivertórico enquanto o **SYSTEM_VERSIONING** estiver **ON** para limpar as partes dos dados de histórico que já não são relevantes.  
  
    -   Não há permestiversão para o**SWITCH IN** enquanto o **SYSTEM_VERSIONING** estiver **ON**, pois isso pode invalidar a consistência dos dados temporais.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
