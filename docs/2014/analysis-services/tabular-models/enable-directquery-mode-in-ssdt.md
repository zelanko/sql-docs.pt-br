---
title: Habilitar o modo de design do DirectQuery (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 965a3a7c1bfa9549793690e92760ce39f147e0d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067202"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>Habilitar o modo de design de DirectQuery (SSAS tabular)
  Para criar um modelo no modo DirectQuery, primeiro altere o ambiente de tempo de design para que ele ofereça suporte ao usuário do modo DirectQuery. Quando você faz isso, o designer também executa as seguintes ações:  
  
-   Habilitar o uso de propriedades de implantação do DirectQuery.  
  
-   Alterar o banco de dados do workspace para que seja executado em um modo híbrido que utiliza o cache para design. Quando você de fato implanta o modelo, o modo retorna ao valor especificado nas propriedades de implantação do projeto.  
  
-   Desabilitar recursos de design que sejam incompatíveis com o modo DirectQuery.  
  
-   Validar o modelo existente.  
  
 Este procedimento descreve como habilitar o modo DirectQuery no designer.  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>Para habilitar o uso do DirectQuery em um modelo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o arquivo de solução.  
  
2.  No Pesquisador de Objetos, clique duas vezes no arquivo Model.bim.  
  
3.  No painel **Propriedades** , altere a propriedade, **DirectQueryMode**, para **Ativado**.  
  
4.  Em caso de erros, no Visual Studio, abra a **Lista de Erros** e resolva os problemas que possam impedir a alternância do modelo para o modo DirectQuery.  
  
## <a name="see-also"></a>Consulte Também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](directquery-mode-ssas-tabular.md)  
  
  
