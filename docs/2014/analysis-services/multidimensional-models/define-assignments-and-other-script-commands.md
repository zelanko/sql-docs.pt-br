---
title: Definir atribuições e outros comandos de Script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- empty scripts [Analysis Services]
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [Analysis Services], calculations
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e95dff588932bc7885d2501e3d24cc643ae10272
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241157"
---
# <a name="define-assignments-and-other-script-commands"></a>Definir atribuições e outros comandos de script
  Para criar um script vazio, no Designer de Cubo, na guia **Cálculos** , clique no ícone **Novo ScriptCommand** na barra de ferramentas. Quando você criar um novo script, inicialmente, ele será exibido com um título em branco no painel **Organizador de Script** da guia Cálculos. Os caracteres que você digitar no painel Expressões de Cálculo serão visíveis como o nome do item no **Organizador de Script**. Portanto, convém digitar um nome comentado na primeira linha para facilitar a identificação do script no painel **Organizador de Script** . Para obter mais informações, consulte [Introdução ao script MDX no Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892). Para obter mais informações sobre problemas de desempenho relacionadas a cálculos e consultas MDX, consulte a seção "Writing Efficient MDX" na [SQL Server 2005 Analysis Services Performance Guide](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
> [!IMPORTANT]  
>  Quando você inicialmente muda para a guia **Cálculos** do Designer de Cubo, o painel **Organizador de Script** contém um único script com um comando CALCULATE. O comando CALCULATE controla a agregação das células do cubo e deve ser editado somente se você pretender especificar manualmente como o cubo será agregado.  
  
 Você pode usar o painel Expressões de Cálculo para construir uma expressão em sintaxe MDX. Ao criar a expressão, você pode copiar ou arrastar os componentes, funções e modelos do cubo do painel **Ferramentas de Cálculo** para o painel Expressões de Cálculo. Isso adicionará o script do item ao painel Expressões de Cálculo no local para onde você o arrastar ou copiar. Substitua os argumentos e seus delimitadores (« e ») pelos valores apropriados.  
  
> [!IMPORTANT]  
>  Ao gravar uma expressão que contém várias instruções usando o painel Expressões de Cálculo, certifique-se de que todas as linhas do script MDX, exceto a última, terminam com um ponto-e-vírgula (;). Os cálculos são concatenados em um único script MDX e cada script possui um ponto-e-vírgula anexado a ele para garantir a compilação correta do script MDX. Se você adicionar um ponto-e-vírgula à última linha do script no painel Expressões de Cálculo, o cubo será construído e implantado corretamente, mas não será possível executar consultas nele.  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos em modelos multidimensionais](calculations-in-multidimensional-models.md)  
  
  
