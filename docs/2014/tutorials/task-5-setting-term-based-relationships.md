---
title: 'Tarefa 5: Definindo o termo relações baseadas em | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0e9a6a1a96d208077e70c0cf1835cff6e34650dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489116"
---
# <a name="task-5-setting-term-based-relationships"></a>Tarefa 5: Definir relações baseadas em termos
  Nesta tarefa, você define algumas relações baseadas em termos para obter valores para o **Supplier Name** domínio. Uma relação baseada em termo permite que você faça uma correção para um termo que faz parte de um valor em um domínio. Elas permitem que diversos valores idênticos, exceto pela ortografia de uma parte comum deles, sejam considerados como sinônimos idênticos. Por exemplo, **Inc** pode ser corrigido para **Incorporated**. O DQS usa essas relações nos processos de descoberta de conhecimento, limpeza ou correspondência. Ver [criar relações baseadas em termos](https://msdn.microsoft.com/library/hh510404.aspx) para obter mais detalhes.  
  
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
  
  
