---
title: Criar credencial – autenticar no Armazenamento do Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6de7b5c8f9cdc7162eb9c6a8ddd214d0486255c6
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175959"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Criar credencial - autenticar no Armazenamento do Azure
  Use a caixa de diálogo **Backup para URL – Criar Credencial** para criar uma nova Credencial do SQL.  
  
 Ao usar essa caixa de diálogo para criar uma credencial, você deve fornecer um certificado de gerenciamento do Azure adicionado ao repositório de certificados local ou um perfil de publicação baixado em seu computador para validar a assinatura e as informações da conta de armazenamento.  
  
 **CREDENCIAL DO SQL**  
 Especifica o nome da Credencial do SQL que você quer criar.  
  
## <a name="azure-credentials"></a>Credenciais do Azure  
 **Certificado de Gerenciamento**  
 Use esta opção para especificar um certificado do repositório de certificados local que corresponda ao certificado de gerenciamento do Azure. Para obter mais informações sobre o certificado de gerenciamento do Azure, consulte [criar e carregar um certificado de gerenciamento para o Azure](https://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Assinatura**  
 Selecione, digite ou cole sua ID de assinatura do Azure que corresponda ao certificado de gerenciamento do repositório de certificados local.  
  
 **Perfil de Publicação**  
 Use essa opção se você tiver um perfil de publicação baixado no seu computador. Se você usar essa opção, a ID da assinatura e o certificado serão automaticamente populados.  
  
> [!CAUTION]  
>  No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Conta de Armazenamento  
 Selecione a conta de armazenamento que você deseja usar para armazenar os arquivos de backup.  
  
  
