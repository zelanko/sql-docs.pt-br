---
title: Conectar ao Armazenamento do Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-f1
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73d0359d7bfdea03544244939ebb08de112bc37b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-microsoft-azure-storage"></a>Conectar ao Armazenamento do Microsoft Azure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use a caixa de diálogo **Conexão de Armazenamento do Windows Azure** para especificar uma conta de armazenamento e validar sua conexão com o Windows Azure.  
  
## <a name="options"></a>Opções  
Especifique as informações a seguir sobre sua conta do Windows Azure e clique em **Avançar** para continuar.  
  
1.  **Conta de Armazenamento** – Especifique o nome da conta de armazenamento.

   >[!NOTE]
   > Você só pode se conectar a [Contas de Armazenamento de Uso Geral](https://docs.microsoft.com/en-us/azure/storage/storage-introduction#introducing-the-azure-storage-services). Conectar-se a outros tipos de contas de armazenamento pode gerar um erro similar ao seguinte:
   >
   >  O valor de um dos cabeçalhos HTTP não está no formato correto. (Microsoft.SqlServer.StorageClient).
   >
   >  O servidor remoto retornou um erro: (400) Solicitação Incorreta. (Sistema)

2.  **Chave de Conta** – Especifique a chave de conta para a conta de armazenamento especificada.  
  
3.  **Use pontos de extremidade seguros (HTTPS)** – Esta opção utiliza a comunicação criptografada e a identificação segura de um servidor Web de rede.  
  
4.  **Salvar chave de conta** – Esta opção salva sua senha em um arquivo criptografado.  
  
