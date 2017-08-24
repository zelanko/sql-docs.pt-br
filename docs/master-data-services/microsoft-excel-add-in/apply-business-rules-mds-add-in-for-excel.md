---
title: "Aplicar regras de negócio (suplemento MDS para Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7bcf554389f2e768b4d49741b00bcb829a600aa0
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>Aplicar regras de negócio (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , aplique regras de negócio quando desejar validar dados e confirmar se eles são válidos. Você pode corrigir as validações e republicar os dados.  
  
> [!NOTE]  
>  A validação dos dados ocorre automaticamente quando você os publica. Para obter mais informações, consulte [Validação &#40;Master Data Services&#41;](../../master-data-services/validation-master-data-services.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter acesso à área funcional do **Gerenciador** .  
  
-   Você deve ter uma planilha ativa que contenha dados gerenciados no MDS.  
  
### <a name="to-apply-business-rules"></a>Para aplicar regras de negócio  
  
1.  No grupo **Publicar e Validar** , clique em **Aplicar Regras**.  
  
    > [!NOTE]  
    >  O número de membros (linhas) que são validados de uma vez depende de uma configuração no [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, consulte [Configurações de regras de negócio](../../master-data-services/system-settings-master-data-services.md#BusinessRules).  
  
2.  Os dados são validados em relação às regras de negócio e duas colunas de status são exibidas. Se essas colunas não forem exibidas automaticamente, no grupo **Publicar e Validar** , clique em **Mostrar Status** para exibi-las.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
