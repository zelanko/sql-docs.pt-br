---
title: "Definir o per&#237;odo de reten&#231;&#227;o de distribui&#231;&#227;o para publica&#231;&#245;es transacionais (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "períodos de retenção de transação [replicação do SQL Server]"
  - "períodos de retenção [replicação do SQL Server]"
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Definir o per&#237;odo de reten&#231;&#227;o de distribui&#231;&#227;o para publica&#231;&#245;es transacionais (SQL Server Management Studio)
  Especifique o período de retenção de distribuição mínimo e o período de retenção máximo da distribuição sobre o **Propriedades de banco de dados de distribuição - \< Banco_de_dados_de_distribuição>** caixa de diálogo. Está disponível na **geral** página o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar o distribuidor e propriedades do publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### Para especificar o período de retenção de distribuição  
  
1.  Na **geral** página do **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique no botão Propriedades (**...**) para o banco de dados de distribuição.  
  
2.  Para especificar o período mínimo de retenção de distribuição, insira um valor na caixa **Pelo menos** ; para especificar o período máximo de retenção de distribuição, insira um valor na caixa **Mas não mais de** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Validade e desativação de assinatura](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  