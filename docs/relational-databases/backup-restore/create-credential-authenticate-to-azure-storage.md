---
title: Criar credencial – autenticar no Armazenamento do Azure | Microsoft Docs
description: No SQL Server, use a página Criar Credencial da caixa de diálogo Backup de Banco de Dados para fornecer um Certificado de Gerenciamento do Azure para validar sua conexão.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d3804de9de13720d5d7813d54bf5f8962b5e2992
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748421"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>Criar credencial - autenticar no Armazenamento do Azure
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a caixa de diálogo **Backup para URL – Criar Credencial** para criar uma nova Credencial do SQL.  
  
 Ao usar essa caixa de diálogo para criar uma credencial, você precisa fornecer um Certificado de Gerenciamento do Azure adicionado ao repositório de certificados local ou a um perfil de publicação baixado em seu computador para validar a assinatura e as informações de conta de armazenamento.  
  
 **CREDENCIAL DO SQL**  
 Especifica o nome da Credencial do SQL que você quer criar.  
  
## <a name="azure-credentials"></a>Credenciais do Azure  
 **Certificado de Gerenciamento**  
 Use essa opção para especificar um certificado do repositório de certificados local que corresponda ao certificado de gerenciamento do Azure. Para obter mais informações sobre o certificado de gerenciamento do Azure, confira [Criar e carregar um certificado de gerenciamento para o Azure](https://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Assinatura**  
 Selecione, digite ou cole a ID de assinatura do Azure que corresponde ao certificado de gerenciamento do repositório local de certificados.  
  
 **Perfil de Publicação**  
 Use essa opção se você tiver um perfil de publicação baixado no seu computador. Se você usar essa opção, a ID da assinatura e o certificado serão automaticamente populados.  
  
> [!CAUTION]  
>  No momento, o SQL Server oferece suporte à versão do perfil de publicação 2.0. Para baixar a versão com suporte do perfil de publicação, consulte [Download do perfil de publicação 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Conta de Armazenamento  
 Selecione a conta de armazenamento que você deseja usar para armazenar os arquivos de backup.  
  
  
