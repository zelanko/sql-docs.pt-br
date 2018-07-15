---
title: Aplicar regras de negócio (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9f1db21079b7c07394a149b173195ed8fca56d5e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254738"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>Aplicar regras de negócio (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , aplique regras de negócio quando desejar validar dados e confirmar se eles são válidos. Você pode corrigir as validações e republicar os dados.  
  
> [!NOTE]  
>  A validação dos dados ocorre automaticamente quando você os publica. Para obter mais informações, consulte [Procedimento armazenado de validação &#40;Master Data Services&#41;](../validation-stored-procedure-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter acesso à área funcional do **Gerenciador** .  
  
-   Você deve ter uma planilha ativa que contenha dados gerenciados no MDS.  
  
### <a name="to-apply-business-rules"></a>Para aplicar regras de negócio  
  
1.  No grupo **Publicar e Validar** , clique em **Aplicar Regras**.  
  
    > [!NOTE]  
    >  O número de membros (linhas) que são validados de uma vez depende de uma configuração no [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, consulte [Configurações de regras de negócio](../system-settings-master-data-services.md#BusinessRules).  
  
2.  Os dados são validados em relação às regras de negócio e duas colunas de status são exibidas. Se essas colunas não forem exibidas automaticamente, no grupo **Publicar e Validar** , clique em **Mostrar Status** para exibi-las.  
  
## <a name="see-also"></a>Consulte também  
 [Publicação de dados &#40;suplemento do MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
