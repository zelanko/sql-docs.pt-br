---
title: "Conectar ao Servidor (Oracle), Propriedades da Conex&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.oracleconnection.connectionprops.f1"
helpviewer_keywords: 
  - "caixa de diálogo Conectar ao Servidor, replicação"
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# Conectar ao Servidor (Oracle), Propriedades da Conex&#227;o
  Use o **Propriedades de conexão** guia o **conectar ao servidor** caixa de diálogo para especificar uma opção de publicação **Gateway** ou **Concluir**. Depois que um Publicador é identificado, essa opção não pode ser alterada sem descartar e reconfigurar o Publicador. Para obter mais informações, consulte [Configurar um editor Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## Opções  
 **Tipo de Publicador**  
 Selecione **Gateway** ou **completa**. A opção **Complete** é projetada para fornecer publicações transacionais e de instantâneo com o conjunto completo de recursos com suporte para publicações Oracle. A opção **Gateway** fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas. A opção **Gateway** não poderá ser usada se você planejar publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo se você selecionar **Gateway**.  
  
 **Tempo Limite**  
 Especifique quanto tempo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distribuidor deve tentar se conectar ao editor Oracle antes que ocorra um erro de tempo limite.  
  
## Consulte também  
 [Glossário de termos para publicações Oracle](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Ajuste de desempenho para Editores Oracle](../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)  
  
  