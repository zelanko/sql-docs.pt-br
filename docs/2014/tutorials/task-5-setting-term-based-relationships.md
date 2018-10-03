---
title: 'Tarefa 5: Definindo o termo relações baseadas em | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 122bd2276705e2485afb296adb66accdaf1ccaaf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150076"
---
# <a name="task-5-setting-term-based-relationships"></a>Tarefa 5: Definindo relações baseadas em termos
  Nesta tarefa, você define algumas relações baseadas em termos para obter valores para o **Supplier Name** domínio. Uma relação baseada em termo permite que você faça uma correção para um termo que faz parte de um valor em um domínio. Elas permitem que diversos valores idênticos, exceto pela ortografia de uma parte comum deles, sejam considerados como sinônimos idênticos. Por exemplo, **Inc** pode ser corrigido para **Incorporated**. O DQS usa essas relações nos processos de descoberta de conhecimento, limpeza ou correspondência. Ver [criar relações baseadas em termos](http://msdn.microsoft.com/library/hh510404.aspx) para obter mais detalhes.  
  
1.  Selecione **Supplier Name** na **lista de domínios**.  
  
2.  Alterne para o **relações baseadas em** guia no painel à direita.  
  
3.  Clique em **adicionar nova relação** na barra de ferramentas para adicionar uma relação à tabela.  
  
4.  Tipo **co** para o **valor** campo e **empresa** para o **correto para** campo.  
  
5.  Repita as duas etapas anteriores para os seguintes valores:  
  
    |Valor|Corrigir para|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![Relações baseadas em termos](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "relações baseadas em termos")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 6: Definindo sinônimos](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
