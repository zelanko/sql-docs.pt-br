---
title: Membros de dimensão deduzidos (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: aac7bf7d5ece29122f095f15bde5fa11255baa6c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013383"
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>Membros de Dimensão Deduzidos (Assistente para Dimensões de Alteração Lenta)
  Use a caixa de diálogo **Membros de Dimensão Deduzidos** para especificar opções para a utilização dos membros deduzidos. Membros deduzidos existem quando uma tabela de fatos faz referência a membros de dimensão que ainda não foram carregados. Quando os dados do membro deduzido são carregados, você pode atualizar o registro existente em vez de criar um novo.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Habilitar suporte a membro deduzido**  
 Se optar por habilitar membros deduzidos, você deve selecionar uma das duas opções abaixo.  
  
 **Todas as colunas com um tipo de alteração são nulas**  
 Especifique se deseja inserir valores nulos em todas as colunas com um tipo de alteração no novo registro de membro deduzido.  
  
 **Use uma coluna Booleana para indicar se o registro atual é um membro deduzido**  
 Especifique se deve ser usada uma coluna Booleana para indicar se o registro atual é um membro deduzido.  
  
 **Indicador de membro deduzido**  
 Se você optou por usar uma coluna Booleana para indicar membros deduzidos como descrito acima, selecione a coluna na lista.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  