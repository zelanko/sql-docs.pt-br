---
title: Particionamento com tabelas temporais | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 04/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: cb93e468300aea6a666ad04e9ce6ad20e1b85fc2
ms.contentlocale: pt-br
ms.lasthandoff: 09/29/2017

---
# <a name="partitioning-with-temporal-tables"></a>Particionamento de Tabelas Temporais
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode usar o particionamento na tabela atual e de histórico de forma independente. No entanto, o particionamento não pode ser usado para alterar o conteúdo dos dados sem o controle da versão do sistema.  
  
> [!NOTE]  
>  O particionamento é um recurso do Enterprise Edition no SQL Server 2016 antes do Service Pack 1 e versões anteriores. Há suporte para particionamento em todas as edições no SQL Server 2016 Service Pack 1 e versões posteriores.
  
-   **Tabela atual:**  
  
    -   **SWITCH IN** na tabela atual para facilitar o carregamento de dados e a consulta enquanto o **SYSTEM_VERSIONING** estiver **ON**  
  
    -   **SWITCH OUT** não é permitido enquanto **SYSTEM_VERSIONING** estiver **ON**  
  
-   **Tabela de histórico:**  
  
    -   É possível executar o**SWITCH OUT** na tabela de hestivertórico enquanto o **SYSTEM_VERSIONING** estiver **ON** para limpar as partes dos dados de histórico que já não são relevantes.  
  
    -   Não há permestiversão para o**SWITCH IN** enquanto o **SYSTEM_VERSIONING** estiver **ON**, pois isso pode invalidar a consistência dos dados temporais.  
  
## <a name="did-this-article-help-you-were-listening"></a>Este artigo foi útil para você? Estamos atentos  
 Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Partitioning%20with%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

