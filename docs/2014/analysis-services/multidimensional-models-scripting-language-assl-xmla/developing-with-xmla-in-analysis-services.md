---
title: Desenvolvimento com XMLA em Serviços de Análise | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27b143a9cc5c888c6e464d300d2ccfea114ef9bc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80380677"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Desenvolvendo com XMLA no Analysis Services
  O XMLA (XML for Analysis) é um protocolo XML baseado em SOAP, criado especificamente para acesso a dados universal para qualquer fonte de dados multidimensional padrão que pode ser acessado por meio de uma conexão HTTP. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa o XMLA como seu único protocolo para se comunicar com aplicativos cliente. Basicamente, todas as bibliotecas de cliente com suporte do Analysis Services formulam solicitações e respostas em XMLA.  
  
 Como desenvolvedor, você pode usar o XMLA para integrar um aplicativo cliente ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], sem qualquer dependência das interfaces do .NET Framework ou COM. Os requisitos de aplicativo que incluem a hospedagem em uma ampla variedade de plataformas podem ser atendidos com o uso do XMLA e de uma conexão HTTP com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é totalmente compatível com a especificação 1.1 do XMLA, mas também a estende para habilitar o suporte para definição, manipulação e controle de dados. As extensões do Analysis Services são referidas como ASSL (Analysis Services Scripting Language). Usar XMLA e ASSL juntos habilita uma variedade maior de funcionalidades do que o XMLA fornece sozinho. Para obter mais informações sobre o ASSL, consulte [Developing with Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Gerenciando conexões e sessões &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)|Descreve como se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e como gerenciar sessões e a capacidade de manutenção de status do processo no XMLA.|  
|[Erros de manuseio e avisos &#40;&#41;XMLA](handling-errors-and-warnings-xmla.md)|Descreve como o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna informações de erro e de aviso para métodos e comandos no XMLA.|  
|[Definição e identificação de objetos &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|Descreve identificadores de objetos e referências de objeto, e como usar identificadores e referências em comandos XMLA.|  
|[Gerenciamento de transações &#40;&#41;XMLA](managing-transactions-xmla.md)|Detalhes sobre como usar os comandos [BeginTransaction,](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla) [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)e [Rollback Transaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) para definir e gerenciar explicitamente uma transação na sessão XMLA atual.|  
|[Cancelamento de comandos &#40;&#41;XMLA](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Descreve como usar o comando [Cancelar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)para cancelar comandos, sessões e conexões no XMLA.|  
|[Realizando operações em lote &#40;&#41;XMLA](performing-batch-operations-xmla.md)|Descreve como usar o comando [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) para executar vários comandos XMLA, em série ou em paralelo, dentro da mesma transação ou como transações separadas, usando um único método XMLA [Execute.](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)|  
|[Criação e alteração de objetos &#40;&#41;XMLA](creating-and-altering-objects-xmla.md)|Descreve como usar os comandos [Criar,](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) [Alterar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)e [Excluir,](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) juntamente com os elementos ASSL (Analysis Services [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language, linguagem de script de serviços de análise), para definir, alterar ou remover objetos de uma instância.|  
|[Bloqueio e desbloqueio de bancos de dados &#40;&#41;XMLA](locking-and-unlocking-databases-xmla.md)|Detalhes de [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) como usar os comandos Bloquear [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [Desbloquear](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) para bloquear e desbloquear um banco de dados.|  
|[Processando objetos &#40;XMLA&#41;](processing-objects-xmla.md)|Descreve como usar [Process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) o comando Processar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para processar um objeto.|  
|[Mesclação de partições &#40;&#41;XMLA](merging-partitions-xmla.md)|Descreve como usar o comando [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mesclar partições em uma instância.|  
|[Projetando Agregações &#40;&#41;XMLA](designing-aggregations-xmla.md)|Descreve como usar o comando [DesignAggregations,](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) seja no modo iterativo ou em lote, para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]projetar agregações para um design de agregação em .|  
|[Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](backing-up-restoring-and-synchronizing-databases-xmla.md)|Descreve como usar os comandos [Backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) e [Restauração](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) para fazer backup e restaurar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados a partir de um arquivo de backup.<br /><br /> Também descreve como usar o comando [Sincronizar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) para sincronizar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados com um banco de dados existente na mesma instância ou em uma instância diferente.|  
|[Inserir, atualizar e soltar membros &#40;o XMLA&#41;](inserting-updating-and-dropping-members-xmla.md)|Descreve como usar os comandos [Inserir,](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla) [Atualizar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)e [Soltar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) para adicionar, alterar ou excluir membros de uma dimensão ativada por gravação.|  
|[Atualizar células &#40;&#41;XMLA](updating-cells-xmla.md)|Descreve como usar o comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) para alterar os valores das células em uma partição ativada por gravação.|  
|[Gerenciamento de caches &#40;&#41;XMLA](managing-caches-xmla.md)|Detalhes de como usar o comando [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) para limpar os caches dos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.|  
|[Rastreamentos de monitoramento &#40;&#41;XMLA](monitoring-traces-xmla.md)|Descreve como usar o comando [Assinar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) para assinar e monitorar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] um rastreamento existente em uma instância.|  
  
## <a name="data-mining-with-xmla"></a>Mineração de dados com o XMLA  
 O XML for Analysis dá suporte completo a conjuntos de linhas do esquema de mineração de dados. Esses conjuntos de linhas fornecem informações para consultar modelos de mineração de dados usando o método [Discover.](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) Para obter mais informações sobre conjuntos de linhas de esquema de mineração de dados, consulte [Conjuntos de linhas de esquema de mineração de dados](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 Para obter mais informações sobre o DMX, consulte [Extensões de mineração de dados &#40;DMX&#41; Reference](/sql/dmx/data-mining-extensions-dmx-reference).  
  
## <a name="namespace-and-schema"></a>Namespace e esquema  
  
### <a name="namespace"></a>Namespace  
 O esquema definido nesta especificação usa o `https://schemas.microsoft.com/AnalysisServices/2003/Engine` namespace XML e a abreviação padrão "DDL".  
  
### <a name="schema"></a>Esquema  
 A definição de um esquema da linguagem XSD para a linguagem de definição do objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] baseia-se na definição dos elementos de esquema e na hierarquia desta seção.  
  
## <a name="extensibility"></a>Extensibilidade  
 A extensibilidade do esquema da linguagem de definição do objeto é fornecida por meio de um elemento do `Annotation` incluído em todos os objetos. Este elemento pode conter qualquer XML válido de qualquer namespace XML (diferente do namespace de destino que define o DDL), e está sujeito às seguintes regras:  
  
-   O XML pode conter somente elementos.  
  
-   Cada elemento deve ter um nome exclusivo. É recomendado que o valor de `Name` faça referência ao namespace de destino.  
  
 Estas regras são impostas para que o conteúdo da marca `Annotation` seja exposto como um conjunto de pares Nome/Valor por meio do DSO 9.0 (Decision Support Objects).  
  
 Os comentários e o espaço em branco na marca `Annotation` que não forem incluídos com um elemento filho podem não ser preservados. Além disso, todos os elementos devem ser leitura-gravação; elementos somente de leitura são ignorados.  
  
 O esquema de linguagem de definição do objeto é fechado, sendo que o servidor não permite a substituição de tipos derivados para elementos definidos no esquema. Dessa forma, o servidor só aceitará o conjunto de elementos definido aqui e nenhum outro elemento ou atributo. Elementos desconhecidos farão com que o mecanismo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gere um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvimento com a linguagem de script de serviços de análise &#40;&#41;ASSL](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Noções básicas sobre a arquitetura do Microsoft OLAP](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
