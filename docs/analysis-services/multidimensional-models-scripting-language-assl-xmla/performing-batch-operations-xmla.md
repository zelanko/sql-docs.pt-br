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
ms.openlocfilehash: 9cb2983bbf03256839870961f40a018997544ff0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="performing-batch-operations-xmla"></a>Executando operações em lote (XMLA)
  Você pode usar o [lote](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) do XML for Analysis (XMLA) para executar vários comandos XMLA usando um único XMLA [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método. Você pode executar vários comandos contidos no **lote** comando como uma única transação ou em transações individuais para cada comando, em série ou em paralelo. Você também pode especificar associações fora de linha e outras propriedades no **lote** comando para processar vários [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Executando comandos em lote transacionais e não transacionais  
 O **lote** comando executa comandos em uma das duas maneiras:  
  
 **Transacional.**  
 Se o **transação** atributo do **lote** estiver definido como true, o **lote** comando executar comandos de todos os comandos contidos pelo **lote** comando em uma única transação – um *transacional* em lotes.  
  
 Se qualquer comando falhar em um lote transacional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reverterá qualquer comando no **lote** comandos executados antes do comando que falhou e o **lote** comando encerra imediatamente. Quaisquer comandos no **lote** comando que ainda não foram executados não são executados. Após o **lote** comando termina, o **lote** comando relata os erros que ocorreram para o comando falha.  
  
 **Não transacional**  
 Se o **transação** atributo é definido como false, o **lote** comando executa cada comando contido pelo **lote** comando em uma transação separada – um  *não transacionais* em lotes. Se qualquer comando falhar em um lote não transacional, o **lote** comando continuará a executar comandos após o comando que falhou. Após o **lote** comando tenta executar todos os comandos que o **lote** comando contém, o **lote** comando relata os erros que ocorreram.  
  
 Todos os resultados retornados por comandos contidos em um **lote** comando são retornados na mesma ordem em que os comandos contidos no **lote** comando. Os resultados retornados por uma **lote** comando variam com base em se o **lote** comando é transacional ou não transacional.  
  
> [!NOTE]  
>  Se um **lote** comando contém um comando que não retorna saída, como o [bloqueio](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) comando e que o comando executado com êxito, o **lote** comando retorna vazio [raiz](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento dentro do elemento de resultados. Vazio **raiz** elemento garante que cada comando contido em um **lote** comando pode ser correspondido com apropriada **raiz** elemento para resultados desse comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Retornando resultados a partir de resultados em lote transacionais  
 Os resultados de comandos executados em um lote transacional não são retornados até que todo o **lote** comando for concluído. Os resultados não são retornados após cada comando ser executado porque qualquer comando que falhar em um lote transacional faria com que todo o **lote** comando e os comandos a serem revertidas. Se todos os comandos, iniciar e executar com êxito, o [retornar](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md) elemento do [ExecuteResponse](../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento retornado pelo **Execute** método para o **em lotes**  comando contém um [resultados](../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md) elemento, que por sua vez, contém um **raiz** elemento para cada comando executado com êxito dentro do **lote** comando. Se qualquer comando do **lote** comando não pode ser iniciado ou não for concluída, o **Execute** método retornará uma falha SOAP para o **lote** comando que contém o erro da comando que falhou.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Retornando resultados a partir de resultados em lote não transacionais  
 Resultados de comandos executados em um lote não transacional são retornados na ordem em que os comandos estão contidos dentro do **lote** comando e como eles são retornados por cada comando. Se nenhum comando contido no **lote** comando pode ser iniciado com êxito, o **Execute** método retornará uma falha SOAP que contém um erro para o **lote** comando. Se pelo menos um comando foi iniciado com êxito, o **retornar** elemento do **ExecuteResponse** elemento retornado pelo **Execute** método para o **em lotes**  comando contém um **resultados** elemento, que por sua vez, contém um **raiz** elemento para cada comando contido no **lote** comando . Se um ou mais comandos em um lote não transacional não pode ser iniciados ou não for concluída, o **raiz** elemento desse comando com falha contém um [erro](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento que descreve o erro.  
  
> [!NOTE]  
>  Desde que pelo menos um comando em um lote não transacional pode ser iniciado, o lote não transacional é considerado executou com êxito, mesmo se todos os comandos contidos no lote não transacional retornará um erro nos resultados do **em lotes**  comando.  
  
## <a name="using-serial-and-parallel-execution"></a>Usando a execução em série ou em paralelo  
 Você pode usar o **lote** comandos de comando para executar incluídos em série ou em paralelo. Quando os comandos são executados em série, o próximo comando incluído no **lote** comando não pode iniciar até que o comando atualmente em execução no **lote** comando for concluído. Quando os comandos são executados em paralelo, vários comandos podem ser executados simultaneamente pelo **lote** comando.  
  
 Para executar comandos em paralelo, adicione os comandos a serem executados em paralelo para o [paralela](../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) propriedade o **lote** comando. Atualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] só pode executar contíguas, sequencial [processo](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comandos em paralelo. Qualquer outro comando XMLA, como [criar](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) ou [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), incluído no **paralela** propriedade é executada em série.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta executar **processo** comandos incluídos no **paralela** propriedade em paralelo, mas não pode garantir que todos os incluídos **processo** comandos podem ser executados em paralelo. A instância analisa cada **processo** comando e, se a instância determina que o comando não pode ser executado em paralelo, o **processo** comando é executado em série.  
  
> [!NOTE]  
>  Para executar comandos em paralelo, o **transação** atributo do **lote** comando deve ser definido como true, pois [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte a apenas uma transação ativa por conexão e não transacionais lotes executam cada comando em uma transação separada. Se você incluir o **paralela** propriedade em um lote não transacional, um erro ocorre.  
  
### <a name="limiting-parallel-execution"></a>Limitando a execução em paralelo  
 Um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância tenta executar quantos **processo** comandos em paralelo possível, até os limites do computador no qual a instância é executada. Você pode limitar o número de execução simultaneamente **processo** comandos definindo o **maxParallel** atributo do **paralela** propriedade para um valor que indica o número máximo de **processo** comandos que podem ser executados em paralelo.  
  
 Por exemplo, um **paralela** propriedade contém os seguintes comandos em sequência listada:  
  
1.  **Criar**  
  
2.  **Processar**  
  
3.  **Alter**  
  
4.  **Processar**  
  
5.  **Processar**  
  
6.  **Processar**  
  
7.  **Delete (excluir) (excluir)**  
  
8.  **Processar**  
  
9. **Processar**  
  
 O **maxParalle**atributo l deste **paralela** estiver definida como 2. Dessa forma, a instância executa as listas de comandos anteriores como descrito na lista seguinte:  
  
-   Comando 1 é executado em série porque o comando 1 é um **criar** comando e somente **processo** comandos podem ser executados em paralelo.  
  
-   Comando 2 é executado em série após a conclusão do comando 1.  
  
-   Comando 3 é executado em série após a conclusão do comando 2.  
  
-   Comandos 4 e 5 são executados em paralelo após a conclusão do comando 3. Embora o comando 6 também seja um **processo** de comando, o comando 6 não pode executar em paralelo com comandos 4 e 5 porque o **maxParallel** estiver definida como 2.  
  
-   O comando 6 é executado em série após a conclusão dos comandos 4 e 5.  
  
-   O comando 7 é executado em série após a conclusão do comando 6.  
  
-   Os comandos 8 e 9 são executados em paralelo após a conclusão do comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Usando o comando em lotes para processar objetos  
 O **lote** comando contém várias propriedades e atributos opcionais especificamente incluídos para oferecer suporte a processamento múltiplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] projetos:  
  
-   O **ProcessAffectedObjects** atributo do **lote** comando indica se a instância também deverá processar qualquer objeto que exija o reprocessamento como resultado de uma **processo** comando incluído no **lote** comando de processamento de um objeto especificado.  
  
-   O [associações](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) propriedade contém uma coleção de associações fora de linha usado por todos os **processo** comandos no **lote** comando.  
  
-   O [fonte de dados](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md) propriedade contém uma associação fora de linha para uma fonte de dados usada por todos os **processo** comandos no **lote** comando.  
  
-   O [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) propriedade contém uma associação fora de linha para uma exibição da fonte de dados usada por todos os **processo** comandos no **lote** comando.  
  
-   O [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) propriedade especifica o modo no qual o **lote** comando manipula erros encontrados por todos os **processo** comandos contidos no **Lote** comando.  
  
    > [!IMPORTANT]  
    >  Um **processo** comando não pode incluir o **associações**, **DataSource**, **DataSourceView**, ou **ErrorConfiguration**  propriedades, se o **processo** comando está contido em um **lote** comando. Se for necessário especificar essas propriedades para um **processo** command, forneça as informações necessárias nas propriedades correspondentes do **lote** comando que contém o **processo** comando.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento batch & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Processar o elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)   
 [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
