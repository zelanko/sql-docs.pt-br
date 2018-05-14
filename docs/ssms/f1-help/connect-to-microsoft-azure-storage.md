---
title: Conectar ao Armazenamento do Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-f1
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c43f3a3e6c717947859e9cbfc1b2de0197129c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
