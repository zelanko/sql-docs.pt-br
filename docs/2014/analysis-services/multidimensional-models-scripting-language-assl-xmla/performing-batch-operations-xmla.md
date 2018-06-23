---
title: Executando operações em lote (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7f164ca12c1de105bcd73f9b371ff4bfe2e00182
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007155"
---
# <a name="performing-batch-operations-xmla"></a>Executando operações em lote (XMLA)
  Você pode usar o [lote](../xmla/xml-elements-commands/batch-element-xmla.md) do XML for Analysis (XMLA) para executar vários comandos XMLA usando um único XMLA [Execute](../xmla/xml-elements-methods-execute.md) método. Você pode executar vários comandos contidos no comando `Batch` como uma única transação ou em transações individuais para cada comando, em série ou em paralelo. Você também pode especificar associações fora de linha e outras propriedades no `Batch` comando para processar vários [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Executando comandos em lote transacionais e não transacionais  
 O comando `Batch` executa comandos de uma destas maneiras:  
  
 **Transacional.**  
 Se o `Transaction` atributo do `Batch` estiver definido como true, o `Batch` comando executar comandos de todos os comandos contidos pelo `Batch` comando em uma única transação – um *transacional* lote.  
  
 Se qualquer comando falhar em um lote transacional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reverterá qualquer comando no `Batch` comandos executados antes do comando que falhou e o `Batch` comando encerra imediatamente. Qualquer comando de `Batch` que ainda não tiver sido executado não o será. Após o término do comando `Batch`, `Batch` informará qualquer erro ocorrido no comando que falhou.  
  
 **Não transacional**  
 Se o `Transaction` atributo é definido como false, o `Batch` comando executa cada comando contido pelo `Batch` comando em uma transação separada – um *não transacionais* lote. Se qualquer comando falhar em um lote não transacional, `Batch` comando continuará a executar comandos após o que falhou. Depois que o comando `Batch` tenta executar todos os comandos que contidos por `Batch`, o comando `Batch` informará qualquer erro ocorrido.  
  
 Todos os resultados retornados por comandos contidos em um comando `Batch` são retornados na mesma ordem em que os comandos estão contidos em `Batch`. Os resultados retornados por um comando `Batch` variam caso `Batch` seja transacional ou não transacional.  
  
> [!NOTE]  
>  Se um `Batch` comando contém um comando que não retorna saída, como o [bloqueio](../xmla/xml-elements-commands/lock-element-xmla.md) comando e que o comando executado com êxito, o `Batch` comando retorna vazio [raiz](../xmla/xml-elements-properties/root-element-xmla.md) elemento dentro do elemento de resultados. O elemento `root` vazio garante que cada comando contido em um `Batch` possa ser correspondido ao elemento `root` apropriado para os resultados desse comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Retornando resultados a partir de resultados em lote transacionais  
 Os resultados de comandos executados em um lote transacional não são retornados até que todo o comando `Batch` é concluído. Os resultados não são retornados após a execução de cada comando porque qualquer comando que falhar em um lote transacional poderia fazer com que todo o comando `Batch` e os comandos nele contidos fossem revertidos. Se todos os comandos, iniciar e executar com êxito, o [retornar](../xmla/xml-elements-properties/return-element-xmla.md) elemento o [ExecuteResponse](../xmla/xml-elements-objects-executeresponse.md) elemento retornado pelo `Execute` método para o `Batch` comando contém um [resultados](../xmla/xml-elements-properties/results-element-xmla.md) elemento, que por sua vez, contém um `root` elemento para cada comando executado com êxito dentro do `Batch` comando. Se qualquer comando de `Batch` não puder ser iniciado ou se a sua conclusão falhar, o método `Execute` retornará uma falha SOAP para comando `Batch` que contém o erro do comando que falhou.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Retornando resultados a partir de resultados em lote não transacionais  
 Os resultados de comandos executados em um lote não transacional são retornados na ordem em que estão contidos em `Batch` e como são retornados por cada comando. Se nenhum comando contido em `Batch` puder ser iniciado com êxito, o método `Execute` retornará uma falha SOAP com um erro para o comando `Batch`. Se pelo menos um comando for iniciado com êxito, o elemento `return` do elemento `ExecuteResponse` retornado pelo método `Execute` para o comando `Batch` conterá um elemento `results` que, por sua vez, conterá um elemento `root` para cada comando contido em `Batch`. Se um ou mais comandos em um lote não transacional não pode ser iniciados ou não for concluída, o `root` elemento desse comando com falha contém um [erro](../xmla/xml-elements-properties/error-element-xmla.md) elemento que descreve o erro.  
  
> [!NOTE]  
>  Desde que pelo menos um comando de um lote não transacional possa ser iniciado, o lote não transacional terá sua execução considerada como bem-sucedida, mesmo que todos os comandos contidos no lote não transacional retornem um erro nos resultados do comando `Batch`.  
  
## <a name="using-serial-and-parallel-execution"></a>Usando a execução em série ou em paralelo  
 Você pode usar o comando `Batch` para executar comandos incluídos em série ou em paralelo. Quando os comandos são executados em série, o próximo comando incluído em `Batch` não poderá ser iniciado até que o comando em execução em `Batch` seja concluído. Quando os comandos são executados em paralelo, vários deles poderão ser executados simultaneamente por `Batch`.  
  
 Para executar comandos em paralelo, adicione os comandos a serem executados em paralelo para o [paralela](../xmla/xml-elements-properties/parallel-element-xmla.md) propriedade o `Batch` comando. Atualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] só pode executar contíguas, sequencial [processo](../xmla/xml-elements-commands/process-element-xmla.md) comandos em paralelo. Qualquer outro comando XMLA, como [criar](../xmla/xml-elements-commands/create-element-xmla.md) ou [Alter](../xmla/xml-elements-commands/alter-element-xmla.md), incluído no `Parallel` propriedade é executada em série.  
  
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
  
-   Comando 2 é executado em série após a conclusão do comando 1.  
  
-   Comando 3 é executado em série após a conclusão do comando 2.  
  
-   Comandos 4 e 5 são executados em paralelo após a conclusão do comando 3. Embora o comando 6 também seja um comando `Process`, não poderá ser executado em paralelo com os comandos 4 e 5 porque a propriedade `maxParallel` foi definida como 2.  
  
-   O comando 6 é executado em série após a conclusão dos comandos 4 e 5.  
  
-   O comando 7 é executado em série após a conclusão do comando 6.  
  
-   Os comandos 8 e 9 são executados em paralelo após a conclusão do comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Usando o comando em lotes para processar objetos  
 O comando `Batch` contém várias propriedades e atributos opcionais especificamente incluídos para dar suporte ao processamento de vários projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   O atributo `ProcessAffectedObjects` do comando `Batch` indica se a instância também deverá processar qualquer objeto que exija o reprocessamento de um resultado de um comando `Process` incluído no comando `Batch` que está processando um objeto especificado.  
  
-   O [associações](../xmla/xml-elements-properties/bindings-element-xmla.md) propriedade contém uma coleção de associações fora de linha usado por todos os `Process` comandos no `Batch` comando.  
  
-   O [a fonte de dados](../xmla/xml-elements-properties/source-element-xmla.md) propriedade contém uma associação fora de linha para uma fonte de dados usada por todos os `Process` comandos no `Batch` comando.  
  
-   O [DataSourceView](../xmla/xml-elements-properties/datasourceview-element-xmla.md) propriedade contém uma associação fora de linha para uma exibição da fonte de dados usada por todos os `Process` comandos no `Batch` comando.  
  
-   O [ErrorConfiguration](../xmla/xml-elements-properties/errorconfiguration-element-xmla.md) propriedade especifica o modo no qual o `Batch` comando manipula erros encontrados por todos os `Process` comandos contidos no `Batch` comando.  
  
    > [!IMPORTANT]  
    >  Um comando `Process` não poderá incluir as propriedades `Bindings`, `DataSource`, `DataSourceView` ou `ErrorConfiguration`, se o comando `Process` estiver contido em um comando `Batch`. Se você precisar especificar essas propriedades para um comando `Process`, forneça as informações necessárias das propriedades correspondentes do comando `Batch` que contém `Process`.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de lote &#40;XMLA&#41;](../xmla/xml-elements-commands/batch-element-xmla.md)   
 [Processar o elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/process-element-xmla.md)   
 [Processamento de objetos de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  