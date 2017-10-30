---
title: "Noções básicas sobre transformações síncronas e assíncronas | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9cc38505042dadb1b057a737279be82bb7923432
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>Compreendendo as transformações síncronas e assíncronas
  Para compreender a diferença entre uma transformação síncrona e uma assíncrona no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], é mais fácil começar com a transformação síncrona. Se uma transformação síncrona não satisfizer suas necessidades, seu design poderá exigir uma transformação assíncrona.  
  
## <a name="synchronous-transformations"></a>Transformações síncronas  
 Uma transformação síncrona processa linhas de entrada e as transmite no fluxo de dados, uma linha por vez. A saída é síncrona com a entrada, o que significa que ela ocorre ao mesmo tempo. Então, para processar uma determinada linha, a transformação não precisa de informações sobre as demais linhas do conjunto de dados. Na implementação real, as linhas são agrupadas em buffers conforme elas são transmitidas de um componente para o outro, mas esses buffers são transparentes para o usuário e você pode assumir que cada linha é processada separadamente.  
  
 Um exemplo de uma transformação síncrona é a transformação de conversão de dados. Para cada linha de entrada, ela converte o valor na coluna especificada e envia a linha em seu modo. Cada operação de conversão distinta é independente de todas as outras linhas no conjunto de dados.  
  
 Em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de script e programação, você especifica uma transformação assíncrona consultando a ID de entrada do componente e atribuindo-à **SynchronousInputID** propriedade das saídas do componente. Dessa forma, o mecanismo de fluxo de dados é informado a processar cada linha da entrada e a enviar cada linha automaticamente para as saídas especificadas. Se você quiser que todas as linhas vão para todas as saídas, não precisa escrever código adicional para transmitir os dados. Se você usar o **ExclusionGroup** propriedade para especificar que as linhas devem ir somente para um ou outro grupo de saídas, como na transformação divisão condicional, você deve chamar o **DirectRow** método para selecionar o destino apropriado para cada linha. Quando você tem uma saída de erro, você deve chamar **DirectErrorRow** para enviar linhas com problemas para a saída de erro em vez da saída padrão.  
  
## <a name="asynchronous-transformations"></a>Transformações assíncronas  
 Você poder decidir que seu design requer uma transformação assíncrona quando não for possível processar cada linha independentemente de todas as outras linhas. Em outras palavras, você não pode transmitir cada linha no fluxo de dados conforme ela é processada. Em vez disso, deve transmitir os dados de forma assíncrona, ou em um momento diferente da entrada. Por exemplo, os cenários a seguir requerem uma transformação assíncrona:  
  
-   O componente tem que adquirir vários buffers de dados antes de executar seu processamento. Um exemplo é a transformação Classificação, onde o componente tem que processar o conjunto completo de linhas em uma única operação.  
  
-   O componente deve combinar linhas de várias entradas. Um exemplo é a transformação Mesclagem, onde o componente tem que examinar várias linhas de cada entrada e então mesclá-las na ordem classificada.  
  
-   Não há nenhuma correspondência um-para-um entre linhas de entrada e linhas de saída. Um exemplo é a transformação Agregação, onde o componente tem que acrescentar uma linha à saída para reter os valores de agregação computados.  
  
 Em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de script e programação, você especifica uma transformação assíncrona atribuindo um valor de 0 para o **SynchronousInputID** propriedade das saídas do componente. . Dessa forma, o mecanismo de fluxo de dados é informado para enviar cada linha automaticamente para as saídas. Em seguida, você deve gravar código para enviar cada linha de maneira explícita para a saída apropriada, adicionando-o ao novo buffer de saída que é criado para a saída de uma transformação assíncrona.  
  
> [!NOTE]  
>  Como um componente de origem também deve adicionar explicitamente cada linha que lê na fonte de dados para seus buffers de saída, uma fonte parecerá uma transformação com saídas assíncronas.  
  
 Também seria possível criar uma transformação assíncrona que emula uma transformação síncrona copiando cada linha de entrada explicitamente para a saída. Usando essa abordagem, você poderia renomear colunas ou converter tipos ou formatos de dados. No entanto, essa abordagem afeta o desempenho. Você pode obter os mesmos resultados com desempenho melhor usando os componentes internos do Integration Services, como Copiar Coluna ou Conversão de Dados.  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma transformação síncrona com o componente de Script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Criando uma transformação assíncrona com o componente de Script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  

