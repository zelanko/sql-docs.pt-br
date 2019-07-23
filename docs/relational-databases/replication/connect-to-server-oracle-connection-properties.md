---
title: Conectar ao Servidor (Oracle), Propriedades da Conexão | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 44e7d219fefe3a4ffc10f1727738a549d2a1b630
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903089"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Conectar ao Servidor (Oracle), Propriedades da Conexão
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a guia **Propriedades de Conexão** da caixa de diálogo **Conectar ao Servidor** para especificar uma opção de publicação **Gateway** ou **Completa**. Depois que um Publicador é identificado, essa opção não pode ser alterada sem descartar e reconfigurar o Publicador. Para obter mais informações, consulte [Configure an Oracle Publisher](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
## <a name="options"></a>Opções  
 **Tipo de Publicador**  
 Selecione **Gateway** ou **Completa**. A opção **Completa** é projetada para fornecer publicações transacionais e de instantâneo com o conjunto completo de recursos com suporte para publicações Oracle. A opção **Gateway** fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas. A opção **Gateway** não poderá ser usada se você planejar publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo se você selecionar **Gateway**.  
  
 **Tempo Limite**  
 Especifique por quanto tempo o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distribuidor deve tentar se conectar ao Editor Oracle antes da ocorrência de um erro de tempo limite.  
  
## <a name="see-also"></a>Consulte Também  
 [Glossário de termos para publicações Oracle](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Performance Tuning for Oracle Publishers](../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
