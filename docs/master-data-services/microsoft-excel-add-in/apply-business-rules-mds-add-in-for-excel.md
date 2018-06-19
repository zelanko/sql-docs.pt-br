---
title: Aplicar regras de negócio (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3d567df9e64c994255fa51da2f47fb2ac451d695
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404888"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>Aplicar regras de negócio (suplemento MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , aplique regras de negócio quando desejar validar dados e confirmar se eles são válidos. Você pode corrigir as validações e republicar os dados.  
  
> [!NOTE]  
>  A validação dos dados ocorre automaticamente quando você os publica. Para obter mais informações, consulte [Validação &#40;Master Data Services&#41;](../../master-data-services/validation-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter acesso à área funcional do **Gerenciador** .  
  
-   Você deve ter uma planilha ativa que contenha dados gerenciados no MDS.  
  
### <a name="to-apply-business-rules"></a>Para aplicar regras de negócio  
  
1.  No grupo **Publicar e Validar** , clique em **Aplicar Regras**.  
  
    > [!NOTE]  
    >  O número de membros (linhas) que são validados de uma vez depende de uma configuração no [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. Para obter mais informações, consulte [Configurações de regras de negócio](../../master-data-services/system-settings-master-data-services.md#BusinessRules).  
  
2.  Os dados são validados em relação às regras de negócio e duas colunas de status são exibidas. Se essas colunas não forem exibidas automaticamente, no grupo **Publicar e Validar** , clique em **Mostrar Status** para exibi-las.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
