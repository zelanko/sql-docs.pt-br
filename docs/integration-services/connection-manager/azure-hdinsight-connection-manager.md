---
title: "Gerenciador de Conexões do Azure HDInsight | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
caps.latest.revision: 
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ead8a391d34f3d679beee4e85aed5bacd0e1334
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="azure-hdinsight-connection-manager"></a>Gerenciador de Conexões do Azure HDInsight
O **Gerenciador de Conexões do Azure HDInsight** permite que um pacote do SSIS se conecte a um cluster HDInsight do Azure.

O **Gerenciador de Conexões do Azure HDInsight** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para criar e configurar um **Gerenciador de Conexões do Azure HDInsight**, siga as etapas abaixo:

1. Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS**, selecione **AzureHDInsight** e clique em **Adicionar**.
2. Na caixa de diálogo **Editor do Gerenciador de Conexões do Azure HDInsight**, especifique o **Nome DNS de Cluster** (sem o prefixo de protocolo), **Nome de usuário** e **Senha** para o cluster HDInsight ao qual se conectar.
3. Clique em **OK** para fechar a caixa de diálogo.
4. Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .
