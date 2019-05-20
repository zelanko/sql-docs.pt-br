---
title: Gerenciador de conexões de Limpeza DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: faa1eedd-db14-41e5-8e58-8f0f6f561e42
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ceddb40eee5f5eafcc134e4ed434c2dabadd6896
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728277"
---
# <a name="dqs-cleansing-connection-manager"></a>Gerenciador de Conexões de Limpeza DQS

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um gerenciador de conexões de Limpeza DQS permite que um pacote se conecte a um servidor [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]. A transformação de Limpeza DQS usa o gerenciador de conexões de Limpeza DQS.  
  
 Para obter mais informações sobre o Data Quality Services, consulte [Conceitos do Data Quality Services](../../data-quality-services/data-quality-services-concepts.md).  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de Limpeza DQS oferece suporte apenas à Autenticação do Windows.  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas no Deisgner do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte a [Caixa de diálogo Editor de Transformação de Limpeza DQS](../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte a documentação da classe <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> no Guia do Desenvolvedor.  
  
  
