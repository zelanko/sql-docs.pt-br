---
description: Gerenciador de Conexões de Limpeza DQS
title: Gerenciador de conexões de Limpeza DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: faa1eedd-db14-41e5-8e58-8f0f6f561e42
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 33586839b3efb0c8c93786a2e020228a44dc6bbc
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726657"
---
# <a name="dqs-cleansing-connection-manager"></a>Gerenciador de Conexões de Limpeza DQS

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um gerenciador de conexões de Limpeza DQS permite que um pacote se conecte a um servidor [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] . A transformação de Limpeza DQS usa o gerenciador de conexões de Limpeza DQS.  
  
 Para obter mais informações sobre o Data Quality Services, consulte [Conceitos do Data Quality Services](../../data-quality-services/data-quality-services-concepts.md).  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de Limpeza DQS oferece suporte apenas à Autenticação do Windows.  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas no Deisgner do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte a [Caixa de diálogo Editor de Transformação de Limpeza DQS](../data-flow/transformations/dqs-cleansing-transformation.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte a documentação da classe <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> no Guia do Desenvolvedor.  
  
