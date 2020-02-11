---
title: Conectar ao Servidor (Oracle), Propriedades da Conexão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 479b0d562ffb78bc0003ca320eea0a85ab172430
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721685"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Conectar ao Servidor (Oracle), Propriedades da Conexão
  Use a **guia Propriedades de conexão** da caixa de diálogo **conectar ao servidor** para especificar uma opção de publicação de **Gateway** ou **concluída**. Depois que um Publicador é identificado, essa opção não pode ser alterada sem descartar e reconfigurar o Publicador. Para obter mais informações, consulte [Configure an Oracle Publisher](non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
## <a name="options"></a>Opções  
 **Tipo de editor**  
 Selecione **Gateway** ou **Completa**. A opção **Complete** é projetada para fornecer publicações transacionais e de instantâneo com o conjunto completo de recursos com suporte para publicações Oracle. A opção **Gateway** fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas. A opção **Gateway** não poderá ser usada se você planejar publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo se você selecionar **Gateway**.  
  
 **Tempos limite**  
 Especifique por quanto tempo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o distribuidor deve tentar se conectar ao Publicador Oracle antes de ocorrer um erro de tempo limite.  
  
## <a name="see-also"></a>Consulte Também  
 [Glossário de termos para publicações Oracle](non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Ajuste de desempenho para Editores Oracle](non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
