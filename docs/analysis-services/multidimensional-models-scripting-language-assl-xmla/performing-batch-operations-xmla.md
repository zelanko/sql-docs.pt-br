---
title: Executando operações em lote (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c451d13016915c9218efb2963429f8f5a7709e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544229"
---
# <a name="performing-batch-operations-xmla"></a>Executando operações em lote (XMLA)
  Você pode usar o [lote](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando XML for Analysis (XMLA) para executar vários comandos XMLA usando um único XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) método. Você pode executar vários comandos contidos na **lote** comando como uma única transação ou em transações individuais para cada comando, em série ou paralelamente. Você também pode especificar associações fora de linha e outras propriedades na **lote** comando para processar vários [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Executando comandos em lote transacionais e não transacionais  
 O **lote** comando executa comandos em uma das duas maneiras:  
  
 **Transacional.**  
 Se o **transação** atributo do **lote** estiver definido como true, o **lote** executará todos os comandos contidos pelo **lote** comando em uma única transação, uma *transacional* em lotes.  
  
 Se algum comando falhar em um lote transacional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reverterá qualquer comando de **lote** comando executado antes do comando que falhou e o **lote** comando terminará imediatamente. Quaisquer comandos de **lote** comando ainda não foram executados não são executadas. Após o **lote** comando termina, o **lote** comando relata os erros que ocorreram para o comando com falha.  
  
 **Não transacional**  
 Se o **transação** atributo é definido como false, o **lote** comando executa cada comando contido pelo **lote** comando em um separado de uma transação  *não transacionais* em lotes. Se algum comando falhar em um lote não transacional, o **lote** comando continuará a executar comandos após o comando que falhou. Após o **lote** comando tenta executar todos os comandos que o **lote** comando contém, o **lote** comando relata os erros que ocorreram.  
  
 Todos os resultados retornados por comandos contidos em um **lote** comando são retornados na mesma ordem em que os comandos estão contidos na **lote** comando. Os resultados retornados por uma **lote** comando variam com base em se a **lote** comando é transacional ou não transacional.  
  
> [!NOTE]  
>  Se um **lote** comando contém um comando que não retorna saída, como o [bloqueio](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comando e que comando é executado com êxito, o **lote** retornará um [raiz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) elemento dentro do elemento de resultados. A esvaziar **raiz** elemento garante que cada comando contido em um **lote** possa ser correspondido com os devidos **raiz** elemento para obter os resultados desse comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Retornando resultados a partir de resultados em lote transacionais  
 Os resultados de comandos executados em um lote transacional não são retornados até que todo o **lote** comando for concluído. Os resultados não são retornados após a execução de cada comando porque qualquer comando que falhar em um lote transacional faria com que todo o **lote** comando e todos os comandos de recipientes seja revertida. Se todos os comandos iniciar e executar com êxito, o [retornar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) elemento da [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) elemento retornado pela **Execute** método para o **em lotes**  comando contém um [resultados](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) elemento, que por sua vez, contém um **raiz** elemento para cada comando executado com êxito, contido no **dolote** comando. Se qualquer comando do **lote** comando não pode ser iniciado ou não for concluída, o **Execute** método retornará uma falha SOAP para o **lote** comando que contém o erro do comando que falhou.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Retornando resultados a partir de resultados em lote não transacionais  
 Resultados de comandos executados em um lote não transacional são retornados na ordem em que os comandos estão contidos dentro de **lote** comando e como eles são retornados por cada comando. Se nenhum comando contido na **lote** comando pode ser iniciado com êxito, o **Execute** método retornará uma falha SOAP que contém um erro para o **lote** comando. Se pelo menos um comando foi iniciado com êxito, o **retornar** elemento da **ExecuteResponse** elemento retornado pela **Execute** método para o **em lotes**  comando contém um **resultados** elemento, que por sua vez, contém um **raiz** elemento para cada comando contido no **lote** comando . Se um ou mais comandos em um lote não transacional não pode ser iniciados ou não for concluída, o **raiz** elemento para o comando com falha contém um [erro](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) elemento que descreve o erro.  
  
> [!NOTE]  
>  Desde que pelo menos um comando em um lote não transacional pode ser iniciado, o lote não transacional é considerado para executar com êxito, mesmo se todos os comandos contidos no lote não transacional retornará um erro nos resultados do **em lotes**  comando.  
  
## <a name="using-serial-and-parallel-execution"></a>Usando a execução em série ou em paralelo  
 Você pode usar o **lote** comandos de comando para executar incluídos em série ou paralelamente. Quando os comandos são executados em série, o próximo comando incluído na **lote** comando não pode iniciar até que o comando atualmente em execução no **lote** comando for concluído. Quando os comandos são executados em paralelo, vários comandos podem ser executados simultaneamente pela **lote** comando.  
  
 Para executar comandos em paralelo, você adiciona os comandos a serem executados em paralelo para o [paralelas](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) propriedade da **lote** comando. No momento, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] só pode executar contíguos, sequencial [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comandos em paralelo. Qualquer outro comando XMLA, como [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) ou [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), incluído no **paralela** propriedade será executada em série.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta executar todos **processo** comandos incluídos na **paralela** propriedade em paralelo, mas não pode garantir que tudo incluído **processo** comandos podem ser executados em paralelo. A instância analisa cada **processo** comando e, se a instância determina que o comando não pode ser executado em paralelo, o **processo** comando é executado em série.  
  
> [!NOTE]  
>  Para executar comandos em paralelo, o **transação** atributo da **lote** comando deve ser definido como true, pois [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a apenas uma transação ativa por conexão e não transacionais lotes executados cada comando em uma transação separada. Se você incluir a **paralela** propriedade em um lote não transacional, um erro ocorre.  
  
### <a name="limiting-parallel-execution"></a>Limitando a execução em paralelo  
 Uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância tenta executar quantos **processo** comandos em paralelo como for possível, até os limites do computador no qual a instância é executada. Você pode limitar o número de execução simultaneamente **processo** comandos, definindo o **maxParallel** atributo do **paralela** propriedade para um valor que indica o número máximo de **processo** comandos que podem ser executados em paralelo.  
  
 Por exemplo, uma **paralela** propriedade contém os comandos a seguir na sequência listada:  
  
1.  **Criar**  
  
2.  **Processar**  
  
3.  **Alter**  
  
4.  **Processar**  
  
5.  **Processar**  
  
6.  **Processar**  
  
7.  **Delete (excluir)**  
  
8.  **Processar**  
  
9. **Processar**  
  
 O **maxParalle**atributo l isso **paralela** estiver definida como 2. Dessa forma, a instância executa as listas de comandos anteriores como descrito na lista seguinte:  
  
-   Comando 1 é executado em série porque o comando 1 é uma **Create** comando e apenas **processo** comandos podem ser executados em paralelo.  
  
-   Comando 2 é executado em série após a conclusão do comando 1.  
  
-   3 de comando é executado em série após a conclusão do comando 2.  
  
-   Comandos 4 e 5 são executados em paralelo após a conclusão do comando 3. Embora o comando 6 também seja um **processo** de comando, o comando 6 não pode executar em paralelo com comandos 4 e 5 porque o **maxParallel** estiver definida como 2.  
  
-   O comando 6 é executado em série após a conclusão dos comandos 4 e 5.  
  
-   O comando 7 é executado em série após a conclusão do comando 6.  
  
-   Os comandos 8 e 9 são executados em paralelo após a conclusão do comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Usando o comando em lotes para processar objetos  
 O **lote** comando contém várias propriedades e atributos opcionais especificamente incluídos para dar suporte a processamento de vários [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projetos:  
  
-   O **ProcessAffectedObjects** atributo da **lote** comando indica se a instância também deverá processar qualquer objeto que exija o reprocessamento como resultado de uma **processo** comando incluído na **lote** comando de processamento de um objeto especificado.  
  
-   O [associações](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) propriedade contém uma coleção de associações fora de linha usado por todos os **processo** comandos no **lote** comando.  
  
-   O [fonte de dados](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla) propriedade contém uma associação fora de linha para uma fonte de dados usada por todos os **processo** comandos no **lote** comando.  
  
-   O [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) propriedade contém uma associação fora de linha para uma exibição da fonte de dados usada por todos os **processo** comandos no **lote** comando.  
  
-   O [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) propriedade especifica a maneira na qual o **lote** comando manipula erros encontrados por todos os **processo** comandos contidos no **Lote** comando.  
  
    > [!IMPORTANT]  
    >  Um **processo** comando não pode incluir o **associações**, **DataSource**, **DataSourceView**, ou **ErrorConfiguration**  propriedades, se o **processo** comando está contido em uma **lote** comando. Se você precisar especificar essas propriedades para um **processo** de comando, forneça as informações necessárias nas propriedades correspondentes do **lote** comando que contém o **processo** comando.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento do lote &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Processar o elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
