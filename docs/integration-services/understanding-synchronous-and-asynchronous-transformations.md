---
title: Compreender as transformações síncronas e assíncronas | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 81ce27c94fbad5e326f636bfcefb633dbf5ebc52
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296475"
---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>Compreendendo as transformações síncronas e assíncronas

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para compreender a diferença entre uma transformação síncrona e uma assíncrona no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], é mais fácil começar com a transformação síncrona. Se uma transformação síncrona não satisfizer suas necessidades, seu design poderá exigir uma transformação assíncrona.  
  
## <a name="synchronous-transformations"></a>Transformações síncronas  
 Uma transformação síncrona processa linhas de entrada e as transmite no fluxo de dados, uma linha por vez. A saída é síncrona com a entrada, o que significa que ela ocorre ao mesmo tempo. Então, para processar uma determinada linha, a transformação não precisa de informações sobre as demais linhas do conjunto de dados. Na implementação real, as linhas são agrupadas em buffers conforme elas são transmitidas de um componente para o outro, mas esses buffers são transparentes para o usuário e você pode assumir que cada linha é processada separadamente.  
  
 Um exemplo de uma transformação síncrona é a transformação de conversão de dados. Para cada linha de entrada, ela converte o valor na coluna especificada e envia a linha em seu modo. Cada operação de conversão distinta é independente de todas as outras linhas no conjunto de dados.  
  
 Na programação e no script do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], você especifica uma transformação assíncrona consultando a ID de uma entrada de componente e atribuindo-a à propriedade **SynchronousInputID** das saídas do componente. Dessa forma, o mecanismo de fluxo de dados é informado a processar cada linha da entrada e a enviar cada linha automaticamente para as saídas especificadas. Se você quiser que todas as linhas vão para todas as saídas, não precisa escrever código adicional para transmitir os dados. Se você usar a propriedade **ExclusionGroup** para especificar que as linhas devem ir somente para ou outro grupo de saídas, como na transformação Divisão Condicional, você deverá chamar o método **DirectRow** para selecionar o destino apropriado para cada linha. Quando você tiver uma saída de erro, deve chamar **DirectErrorRow** para enviar linhas com problemas para a saída de erro em vez da saída padrão.  
  
## <a name="asynchronous-transformations"></a>Transformações assíncronas  
 Você poder decidir que seu design requer uma transformação assíncrona quando não for possível processar cada linha independentemente de todas as outras linhas. Em outras palavras, você não pode transmitir cada linha no fluxo de dados conforme ela é processada. Em vez disso, deve transmitir os dados de forma assíncrona, ou em um momento diferente da entrada. Por exemplo, os cenários a seguir requerem uma transformação assíncrona:  
  
-   O componente tem que adquirir vários buffers de dados antes de executar seu processamento. Um exemplo é a transformação Classificação, onde o componente tem que processar o conjunto completo de linhas em uma única operação.  
  
-   O componente deve combinar linhas de várias entradas. Um exemplo é a transformação Mesclagem, onde o componente tem que examinar várias linhas de cada entrada e então mesclá-las na ordem classificada.  
  
-   Não há nenhuma correspondência um-para-um entre linhas de entrada e linhas de saída. Um exemplo é a transformação Agregação, onde o componente tem que acrescentar uma linha à saída para reter os valores de agregação computados.  
  
 No script e na programação do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], você especifica uma transformação assíncrona atribuindo um valor 0 à propriedade **SynchronousInputID** das saídas do componente. . Dessa forma, o mecanismo de fluxo de dados é informado para enviar cada linha automaticamente para as saídas. Em seguida, você deve gravar código para enviar cada linha de maneira explícita para a saída apropriada, adicionando-o ao novo buffer de saída que é criado para a saída de uma transformação assíncrona.  
  
> [!NOTE]  
>  Como um componente de origem também deve adicionar explicitamente cada linha que lê na fonte de dados para seus buffers de saída, uma fonte parecerá uma transformação com saídas assíncronas.  
  
 Também seria possível criar uma transformação assíncrona que emula uma transformação síncrona copiando cada linha de entrada explicitamente para a saída. Usando essa abordagem, você poderia renomear colunas ou converter tipos ou formatos de dados. No entanto, essa abordagem afeta o desempenho. Você pode obter os mesmos resultados com desempenho melhor usando os componentes internos do Integration Services, como Copiar Coluna ou Conversão de Dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando uma transformação síncrona com o componente Script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Criar uma transformação assíncrona com o componente Script](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [Desenvolver um componente de transformação personalizado com saídas síncronas](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
