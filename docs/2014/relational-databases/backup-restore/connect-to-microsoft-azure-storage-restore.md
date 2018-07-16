---
title: Conectar-se ao Windows Azure Storage (Restaurar) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 63f7f0e06a94d9d6a05995e9c19f24f0b8d46047
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172897"
---
# <a name="connect-to-windows-azure-storage-restore"></a>Conectar ao Windows Azure Storage (Restaurar)
  A caixa de diálogo permite que você especifique a conexão com as informações da conta de armazenamento do Windows Azure para recuperar o armazenamento de arquivos da conta de armazenamento do Windows Azure. Depois de especificar as informações necessárias, clique em **Conectar** para estabelecer a conexão com o armazenamento do Windows Azure.  
  
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
  
  
