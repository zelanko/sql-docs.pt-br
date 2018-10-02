---
title: Conectar ao Armazenamento do Microsoft Azure | Microsoft Docs
ms.custom: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff61f3f69b5ce5c73a96d6f9c06141e5bd17f75a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47839367"
---
# <a name="connect-to-microsoft-azure-storage"></a>Conectar ao Armazenamento do Microsoft Azure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use a caixa de diálogo **Conexão de Armazenamento do Windows Azure** para especificar uma conta de armazenamento e validar sua conexão com o Windows Azure.  
  
## <a name="options"></a>Opções  
Especifique as informações a seguir sobre sua conta do Windows Azure e clique em **Avançar** para continuar.  
  
1.  **Conta de Armazenamento** – Especifique o nome da conta de armazenamento.

   >[!NOTE]
   > Você só pode se conectar a [Contas de Armazenamento de Uso Geral](https://docs.microsoft.com/azure/storage/storage-introduction#introducing-the-azure-storage-services). Conectar-se a outros tipos de contas de armazenamento pode gerar um erro similar ao seguinte:
   >
   >  O valor de um dos cabeçalhos HTTP não está no formato correto. (Microsoft.SqlServer.StorageClient).
   >
   >  O servidor remoto retornou um erro: (400) Solicitação Incorreta. (Sistema)

2.  **Chave de Conta** – Especifique a chave de conta para a conta de armazenamento especificada.  
  
3.  **Use pontos de extremidade seguros (HTTPS)** – Esta opção utiliza a comunicação criptografada e a identificação segura de um servidor Web de rede.  
  
4.  **Salvar chave de conta** – Esta opção salva sua senha em um arquivo criptografado.  
  
