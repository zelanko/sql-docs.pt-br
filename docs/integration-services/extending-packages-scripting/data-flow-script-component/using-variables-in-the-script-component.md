---
title: "Usando variáveis no componente Script | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bac1e6d96e872be0355282c3e12fc81054ca41cd
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-component"></a>Usando variáveis no componente Script
  As variáveis armazenam valores que um pacote e seus contêineres, tarefas e manipuladores de eventos podem usar em tempo de execução. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Variables](../../../integration-services/integration-services-ssis-variables.md).  
  
 Você pode tornar as variáveis existentes disponíveis para somente leitura ou leitura/gravação por seu script personalizado inserindo listas delimitada por vírgulas de variáveis no **ReadOnlyVariables** e **ReadWriteVariables** campos o **Script** página do **Editor de transformação scripts**. Lembre-se de que os nomes de variáveis diferenciam maiúsculas de minúsculas. Use o **valor** propriedade de leitura e gravação em variáveis individuais. O componente Script trata qualquer bloqueio necessário em segundo plano, à medida que seu script manipula as variáveis em tempo de execução.  
  
> [!IMPORTANT]  
>  A coleção de **ReadWriteVariables** só está disponível na **PostExecute** método para maximizar o desempenho e minimizar o risco de conflitos de bloqueio. Portanto, não será possível incrementar diretamente o valor de uma variável de pacote ao processar cada linha de dados. Incrementar o valor de uma variável local em vez disso e defina o valor da variável de pacote para o valor da variável local no **PostExecute** método depois que todos os dados foram processado. Você também pode usar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> para funcionar nesta limitação, conforme descrito posteriormente neste tópico. Entretanto, gravar diretamente em uma variável de pacote, à medida que cada linha for processada, afetará negativamente o desempenho e aumentará o risco de conflitos de bloqueio.  
  
 Para obter mais informações sobre o **Script** página do **Editor de transformação scripts**, consulte [Configurando o componente Script no Editor de componente de Script](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) e [Editor de transformação scripts &#40; Script de página &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 O componente Script cria uma **variáveis** classe de coleção no **ComponentWrapper** item de projeto com uma propriedade de acessador fortemente tipadas para o valor de cada variável pré-configurada onde a propriedade tem o mesmo nome que a variável em si. Essa coleção é exposta por meio de **variáveis** propriedade do **ScriptMain** classe. A propriedade de acessador fornece permissão somente leitura ou de leitura/gravação ao valor da variável conforme apropriado. Por exemplo, se você tiver adicionado uma variável de inteiro nomeada `MyIntegerVariable` para o **ReadOnlyVariables** lista, você pode recuperar seu valor em seu script usando o código a seguir:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 Você também pode usar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, acessada chamando `Me.VariableDispenser`, para trabalhar com variáveis no componente Script. Neste caso você não está utilizando as propriedades de acessador digitadas e nomeadas para variáveis, mas acessando as variáveis diretamente. Ao usar o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, você deve tratar as semânticas de bloqueio e a conversão de tipos de dados para obter valores variáveis em seu próprio código. Você deve usar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> em vez das propriedades de acessador nomeadas e tipadas, se desejar trabalhar com uma variável que não esteja disponível no tempo de design, mas é criada programaticamente no tempo de execução.  
  
## <a name="see-also"></a>Consulte também  
 [Integration Services &#40; SSIS &#41; Variáveis](../../../integration-services/integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
