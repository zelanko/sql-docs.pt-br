---
title: Criar credencial – autenticar no Armazenamento do Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7cd1ba85ffc3a0531f8891adb91a2beae3e63889
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252248"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Criar credencial - autenticar no Armazenamento do Azure
  Use a caixa de diálogo **Backup para URL – Criar Credencial** para criar uma nova Credencial do SQL.  
  
 Ao usar essa caixa de diálogo para criar uma credencial, você deve fornecer um Certificado de Gerenciamento do Windows Azure adicionado ao repositório de certificados local ou a um perfil de publicação baixado em seu computador para validar a assinatura e as informações de conta de armazenamento.  
  
 **CREDENCIAL DO SQL**  
 Especifica o nome da Credencial do SQL que você quer criar.  
  
## <a name="windows-azure-credentials"></a>Credenciais do Windows Azure  
 **Certificado de Gerenciamento**  
 Use essa opção para especificar um certificado do repositório de certificados local que corresponde ao certificado de gerenciamento do Windows Azure. Para obter mais informações sobre o certificado de gerenciamento do Windows Azure, consulte [Criar e carregar um Certificado de Gerenciamento para o Windows Azure](http://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Assinatura**  
 Selecione, digite ou cole a ID de assinatura do Windows Azure que corresponde ao certificado de gerenciamento do repositório local de certificados.  
  
 **Perfil de Publicação**  
 Use essa opção se você tiver um perfil de publicação baixado no seu computador. Se você usar essa opção, a ID da assinatura e o certificado serão automaticamente populados.  
  
> [!CAUTION]  
>  No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Conta de Armazenamento  
 Selecione a conta de armazenamento que você deseja usar para armazenar os arquivos de backup.  
  
  
