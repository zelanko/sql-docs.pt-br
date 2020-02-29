---
title: Gerenciador de Conexões da Assinatura do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpsubscrconn.f1
- sql11.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 31a24acb49abf4965e18443ef4c46ffd9a16f15c
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176513"
---
# <a name="azure-subscription-connection-manager"></a>Gerenciador de Conexões da Assinatura do Azure
  O Gerenciador de Conexões do Azure HDInsight permite que um pacote do SSIS se conecte a uma assinatura do Azure usando os valores especificados para as propriedades: ID da Assinatura do Azure e Certificado de Gerenciamento.

1.  Na caixa de diálogo **Adicionar Gerenciador de Conexões SSIS** mostrada acima, escolha **Assinatura do Azure**e clique em **Adicionar**.  Você deve ver a caixa de diálogo **Editor do Gerenciador de Conexões da Assinatura do Azure** a seguir.

     ![SSIS-AzureSubscriptionManager](../media/ssis-azuresubscriptionmanager.png "SSIS-AzureSubscriptionManager")

2.  Insira sua ID de assinatura do Azure, que identifica exclusivamente uma assinatura do Azure, em **ID da assinatura do Azure**.  O valor pode ser encontrado no [Portal de Gerenciamento do Azure](https://manage.windowsazure.com) na página **Configurações** :

     ![SSIS-AzureSettings-SubscriptionId](../media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")

3.  Escolha **Local do repositório de certificados de gerenciamento** e **Nome do repositório de certificados de gerenciamento** nas listas suspensas.

4.  Insira **Impressão digital do certificado de gerenciamento** ou clique em **Procurar...** para escolher um certificado no repositório selecionado. O certificado deve ser carregado como um certificado de gerenciamento para a assinatura. Para fazer isso, clique em **Carregar** na página a seguir do Portal do Azure (confira esta [postagem do MSDN](https://msdn.microsoft.com/library/azure/gg551722.aspx) para obter mais detalhes).

     ![SSIS-AzureSettings-certificado remoto](../media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")

5.  Clique em **testar conexão** para testar a conexão.

6.  Clique em **OK** para fechar a caixa de diálogo.


