---
title: Conectar ao Armazenamento do Microsoft Azure (Restaurar) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1e0129c986da132733fc102358229a64e5fbf77
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Conectar ao Armazenamento do Microsoft Azure (Restaurar)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A caixa de diálogo permite que você especifique as informações da conexão com a conta de armazenamento do Microsoft Azure a fim de recuperar o armazenamento de arquivos nessa conta de armazenamento do Microsoft Azure. Depois de especificar as informações necessárias, clique em **Conectar** para estabelecer a conexão com o armazenamento do Windows Azure.  
  
## <a name="windows-azure-storage-account"></a>Conta de armazenamento do Windows Azure Storage  
 **Conta de armazenamento**  
 Selecione, digite ou cole o nome da conta de armazenamento do Windows Azure que você deseja usar. A caixa suspensa lista as contas usadas anteriormente.  
  
 **Chave de conta**  
 Especifique a chave de acesso da conta de armazenamento do Windows Azure.  
  
 Caixa de seleção**Usar pontos de extremidade seguros (HTTPS)**   
 Selecione esta opção para estabelecer uma conexão segura com o armazenamento do Windows Azure – recomendado.  
  
 Caixa de seleção**Salvar chave de conta**   
 Marque esta caixa de seleção se desejar que o SQL Server se lembre da chave de acesso para essa conta de armazenamento.  
  
### <a name="sql-credential"></a>CREDENCIAL DO SQL  
 **Selecionar uma credencial existente**  
 Selecione uma credencial existente do SQL que corresponda à conta de armazenamento e às informações de chave de conta.  
  
 **Criar uma nova credencial**  
 Selecione esta opção para criar uma nova credencial usando a conta de armazenamento e as informações de chave de conta. Especifique o nome da nova credencial no campo de **Nome da Credencial** .  
  
  
