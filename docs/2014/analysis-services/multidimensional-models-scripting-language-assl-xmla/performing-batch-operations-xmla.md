---
title: Executando operações em lote (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bd661506dbb792eb55194c61d7284d619e63a5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702058"
---
# <a name="performing-batch-operations-xmla"></a>Executando operações em lote (XMLA)
  Você pode usar o comando [batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) em XML for Analysis (XMLA) para executar vários comandos XMLA usando um único método XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) . Você pode executar vários comandos contidos no comando `Batch` como uma única transação ou em transações individuais para cada comando, em série ou em paralelo. Você também pode especificar associações fora de linha e outras propriedades `Batch` no comando para processar vários [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Executando comandos em lote transacionais e não transacionais  
 O comando `Batch` executa comandos de uma destas maneiras:  
  
 **Transacional**  
 Se o `Transaction` atributo do `Batch` comando for definido como true, o `Batch` comando executará comandos de todos os comandos contidos pelo `Batch` comando em uma única transação – um lote *transacional* .  
  
 Se qualquer comando falhar em um lote transacional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reverterá qualquer comando no `Batch` comando executado antes do comando que falhou e o `Batch` comando terminará imediatamente. Qualquer comando de `Batch` que ainda não tiver sido executado não o será. Após o término do comando `Batch`, `Batch` informará qualquer erro ocorrido no comando que falhou.  
  
 **Não transacional**  
 Se o `Transaction` atributo for definido como false, o `Batch` comando executará cada comando contido no `Batch` comando em uma transação separada, um lote não *transacional* . Se qualquer comando falhar em um lote não transacional, `Batch` comando continuará a executar comandos após o que falhou. Depois que o comando `Batch` tenta executar todos os comandos que contidos por `Batch`, o comando `Batch` informará qualquer erro ocorrido.  
  
 Todos os resultados retornados por comandos contidos em um comando `Batch` são retornados na mesma ordem em que os comandos estão contidos em `Batch`. Os resultados retornados por um comando `Batch` variam caso `Batch` seja transacional ou não transacional.  
  
> [!NOTE]  
>  Se um `Batch` comando contiver um comando que não retorna uma saída, como o comando [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) , e esse comando for executado com êxito, `Batch` o comando retornará um elemento [raiz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) vazio dentro do elemento results. O elemento `root` vazio garante que cada comando contido em um `Batch` possa ser correspondido ao elemento `root` apropriado para os resultados desse comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Retornando resultados a partir de resultados em lote transacionais  
 Os resultados de comandos executados em um lote transacional não são retornados até que todo o comando `Batch` é concluído. Os resultados não são retornados após a execução de cada comando porque qualquer comando que falhar em um lote transacional poderia fazer com que todo o comando `Batch` e os comandos nele contidos fossem revertidos. Se todos os comandos forem iniciados e executados com êxito, o elemento [Return](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) do elemento [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) retornado `Execute` pelo método para `Batch` o comando conterá um elemento [Results](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) que, por `root` sua vez, conterá um elemento para cada comando `Batch` executado com êxito contido no comando. Se qualquer comando de `Batch` não puder ser iniciado ou se a sua conclusão falhar, o método `Execute` retornará uma falha SOAP para comando `Batch` que contém o erro do comando que falhou.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Retornando resultados a partir de resultados em lote não transacionais  
 Os resultados de comandos executados em um lote não transacional são retornados na ordem em que estão contidos em `Batch` e como são retornados por cada comando. Se nenhum comando contido em `Batch` puder ser iniciado com êxito, o método `Execute` retornará uma falha SOAP com um erro para o comando `Batch`. Se pelo menos um comando for iniciado com êxito, o elemento `return` do elemento `ExecuteResponse` retornado pelo método `Execute` para o comando `Batch` conterá um elemento `results` que, por sua vez, conterá um elemento `root` para cada comando contido em `Batch`. Se um ou mais comandos em um lote não transacional não puderem ser iniciados ou não `root` forem concluídos, o elemento desse comando com falha conterá um elemento de [erro](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) que descreve o erro.  
  
> [!NOTE]  
>  Desde que pelo menos um comando de um lote não transacional possa ser iniciado, o lote não transacional terá sua execução considerada como bem-sucedida, mesmo que todos os comandos contidos no lote não transacional retornem um erro nos resultados do comando `Batch`.  
  
## <a name="using-serial-and-parallel-execution"></a>Usando a execução em série ou em paralelo  
 Você pode usar o comando `Batch` para executar comandos incluídos em série ou em paralelo. Quando os comandos são executados em série, o próximo comando incluído em `Batch` não poderá ser iniciado até que o comando em execução em `Batch` seja concluído. Quando os comandos são executados em paralelo, vários deles poderão ser executados simultaneamente por `Batch`.  
  
 Para executar comandos em paralelo, você adiciona os comandos a serem executados em paralelo à propriedade [Parallel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) do `Batch` comando. Atualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o pode executar apenas comandos de [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) sequenciais e contíguos em paralelo. Qualquer outro comando XMLA, como [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) ou [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), incluído na `Parallel` propriedade é executado em série.  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta executar comandos `Process` incluídos na propriedade `Parallel` em paralelo, mas não pode garantir que todos os comandos `Process` incluídos serão executados em paralelo. A instância analisa cada comando `Process` e, se a instância determinar que o comando não pode ser executado em paralelo, o comando `Process` será executado em série.  
  
> [!NOTE]  
>  Para executar comandos em paralelo, o atributo `Transaction` do comando `Batch` deve ser definido como true porque o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] só dá suporte a uma transação ativa por conexão e lotes não transacionais executam cada comando em uma transação separada. Se você incluir a propriedade `Parallel` em um lote não transacional, ocorrerá um erro.  
  
### <a name="limiting-parallel-execution"></a>Limitando a execução em paralelo  
 Uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta executar quantos comandos `Process` em paralelo como for possível, até os limites do computador em que ela está sendo executada. Você pode limitar o número de comandos `Process` executados simultaneamente por meio da configuração do atributo `maxParallel` da propriedade `Parallel` como um valor indicando o número máximo de comandos `Process` que podem ser executados em paralelo.  
  
 Por exemplo, uma propriedade `Parallel` contém os comandos a seguir na sequência listada:  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 O atributo `maxParalle`l dessa propriedade `Parallel` é definido como 2. Dessa forma, a instância executa as listas de comandos anteriores como descrito na lista seguinte:  
  
-   O comando 1 é executado em série porque é um comando `Create` e somente os comandos `Process` podem ser executados em paralelo.  
  
-   O comando 2 é executado em série após a conclusão do comando 1.  
  
-   O comando 3 é executado em série após a conclusão do comando 2.  
  
-   Os comandos 4 e 5 são executados em paralelo após a conclusão do comando 3. Embora o comando 6 também seja um comando `Process`, não poderá ser executado em paralelo com os comandos 4 e 5 porque a propriedade `maxParallel` foi definida como 2.  
  
-   O comando 6 é executado em série após a conclusão dos comandos 4 e 5.  
  
-   O comando 7 é executado em série após a conclusão do comando 6.  
  
-   Os comandos 8 e 9 são executados em paralelo após a conclusão do comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Usando o comando em lotes para processar objetos  
 O comando `Batch` contém várias propriedades e atributos opcionais especificamente incluídos para dar suporte ao processamento de vários projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   O atributo `ProcessAffectedObjects` do comando `Batch` indica se a instância também deverá processar qualquer objeto que exija o reprocessamento de um resultado de um comando `Process` incluído no comando `Batch` que está processando um objeto especificado.  
  
-   A propriedade [bindings](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) contém uma coleção de associações fora de linha usadas por todos os `Process` comandos no `Batch` comando.  
  
-   A propriedade [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) contém uma associação fora de linha para uma fonte de dados usada por todos os `Process` comandos no `Batch` comando.  
  
-   A propriedade [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) contém uma associação fora de linha para uma exibição da fonte de dados usada por todos os `Process` comandos no `Batch` comando.  
  
-   A propriedade [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) especifica a maneira como o `Batch` comando manipula os erros encontrados por todos `Process` os comandos contidos no `Batch` comando.  
  
    > [!IMPORTANT]  
    >  Um comando `Process` não poderá incluir as propriedades `Bindings`, `DataSource`, `DataSourceView` ou `ErrorConfiguration`, se o comando `Process` estiver contido em um comando `Batch`. Se você precisar especificar essas propriedades para um comando `Process`, forneça as informações necessárias das propriedades correspondentes do comando `Batch` que contém `Process`.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento de lote &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Elemento Process &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Processamento de objeto de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
