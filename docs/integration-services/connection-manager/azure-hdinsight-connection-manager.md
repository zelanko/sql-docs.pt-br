---
title: "Gerenciador de Conexão de HDInsight do Azure | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
caps.latest.revision: 4
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 080cd1184d3c29673ac476d6fe6087b697160544
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-connection-manager"></a>Gerenciador de Conexão de HDInsight do Azure
O **Gerenciador de Conexão do Azure HDInsight** permite que um pacote do SSIS para se conectar a um cluster Azure HDInsight.

O **Gerenciador de Conexão do Azure HDInsight** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para criar e configurar um **Gerenciador de Conexão do Azure HDInsight**, siga as etapas abaixo:

1. No **adicionar Gerenciador de Conexão SSIS** caixa de diálogo, selecione **AzureHDInsight**e clique em **adicionar**.
2. No **Editor do Gerenciador de Conexão de HDInsight do Azure** caixa de diálogo, especifique o **nome DNS de Cluster** (sem o prefixo de protocolo), **Username**, e **senha** para o cluster HDInsight para se conectar ao.
3. Clique em **OK** para fechar a caixa de diálogo.
4. Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .

