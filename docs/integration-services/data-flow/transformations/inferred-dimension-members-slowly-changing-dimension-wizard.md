---
title: Membros de dimensão deduzidos (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c335c99776295d139ed8bca6c49a6a67d5841fce
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35401228"
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>Membros de Dimensão Deduzidos (Assistente para Dimensões de Alteração Lenta)
  Use a caixa de diálogo **Membros de Dimensão Deduzidos** para especificar opções para a utilização dos membros deduzidos. Membros deduzidos existem quando uma tabela de fatos faz referência a membros de dimensão que ainda não foram carregados. Quando os dados do membro deduzido são carregados, você pode atualizar o registro existente em vez de criar um novo.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Habilitar suporte a membro deduzido**  
 Se optar por habilitar membros deduzidos, você deve selecionar uma das duas opções abaixo.  
  
 **Todas as colunas com um tipo de alteração são nulas**  
 Especifique se deseja inserir valores nulos em todas as colunas com um tipo de alteração no novo registro de membro deduzido.  
  
 **Use uma coluna Booleana para indicar se o registro atual é um membro deduzido**  
 Especifique se deve ser usada uma coluna Booleana para indicar se o registro atual é um membro deduzido.  
  
 **Indicador de membro deduzido**  
 Se você optou por usar uma coluna Booleana para indicar membros deduzidos como descrito acima, selecione a coluna na lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
