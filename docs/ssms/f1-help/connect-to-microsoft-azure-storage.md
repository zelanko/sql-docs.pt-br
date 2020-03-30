---
title: Conectar ao Armazenamento do Microsoft Azure
ms.custom: seo-lt-2019
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eb943430136a1406ea18b9c387c98fbec6fd27cf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245019"
---
# <a name="connect-to-microsoft-azure-storage"></a>Conectar ao Armazenamento do Microsoft Azure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use a caixa de diálogo **Conexão de Armazenamento do Microsoft Azure** para especificar uma conta de armazenamento e validar sua conexão com o Azure.  
  
## <a name="options"></a>Opções  
Especifique as informações a seguir sobre sua conta do Azure e clique em **Avançar** para continuar.  
  
1.  **Conta de Armazenamento** – Especifique o nome da conta de armazenamento.

   >[!NOTE]
   > Você só pode se conectar a [Contas de Armazenamento de Uso Geral](https://docs.microsoft.com/azure/storage/storage-introduction#azure-storage-services). Conectar-se a outros tipos de contas de armazenamento pode gerar um erro similar ao seguinte:
   >
   >  O valor de um dos cabeçalhos HTTP não está no formato correto. (Microsoft.SqlServer.StorageClient).
   >
   >  O servidor remoto retornou um erro: (400) Solicitação Incorreta. (Sistema)

2.  **Chave de Conta** – Especifique a chave de conta para a conta de armazenamento especificada.  
  
3.  **Use pontos de extremidade seguros (HTTPS)** – esta opção utiliza a comunicação criptografada e a identificação segura de um servidor Web de rede.  
  
4.  **Salvar chave de conta** – Esta opção salva sua senha em um arquivo criptografado.  
  
