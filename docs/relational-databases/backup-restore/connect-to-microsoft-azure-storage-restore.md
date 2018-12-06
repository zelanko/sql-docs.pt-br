---
title: Conectar ao Armazenamento do Microsoft Azure (Restaurar) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2e8a6d88387fb0674cd8d39f44a30358009e44f9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503971"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Conectar ao Armazenamento do Microsoft Azure (Restaurar)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A caixa de diálogo permite que você especifique a conexão com as informações da conta de armazenamento do Windows Azure para recuperar o armazenamento de arquivos da conta de armazenamento do Windows Azure. Depois de especificar as informações necessárias, clique em **Conectar** para estabelecer a conexão com o armazenamento do Windows Azure.  
  
## <a name="windows-azure-storage-account"></a>Conta de armazenamento do Windows Azure Storage  
 **Conta de armazenamento**  
 Selecione, digite ou cole o nome da conta de armazenamento do Windows Azure que você deseja usar. A caixa suspensa lista as contas usadas anteriormente.  
  
 **Chave de conta**  
 Especifique a chave de acesso da conta de armazenamento do Windows Azure.  
  
 Caixa de seleção**Usar pontos de extremidade seguros (HTTPS)**   
 Selecione esta opção para estabelecer uma conexão segura com o armazenamento do Microsoft Azure – recomendado.  
  
 Caixa de seleção**Salvar chave de conta**   
 Marque esta caixa de seleção se desejar que o SQL Server se lembre da chave de acesso para essa conta de armazenamento.  
  
### <a name="sql-credential"></a>CREDENCIAL DO SQL  
 **Selecionar uma credencial existente**  
 Selecione uma credencial existente do SQL que corresponda à conta de armazenamento e às informações de chave de conta.  
  
 **Criar uma nova credencial**  
 Selecione esta opção para criar uma nova credencial usando a conta de armazenamento e as informações de chave de conta. Especifique o nome da nova credencial no campo de **Nome da Credencial** .  
  
  
