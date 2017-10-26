---
title: "Introdução ao modelo de objeto de tabela (TOM) do Analysis Services AMO | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 57a4a934-ecd0-4365-8147-d36899d86751
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: ab4bfb890124538878fd4d618dee05d393a4864c
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="introduction-to-the-tabular-object-model-tom-in-analysis-services-amo"></a>Introdução ao modelo de objeto de tabela (TOM) no Analysis Services AMO

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  O modelo de objeto de tabela (TOM) é uma extensão da biblioteca do cliente de gerenciamento objeto AMO (Analysis Services), criada para dar suporte a cenários de programação para modelos de tabela criados no nível de compatibilidade 1200 e superior. Como com o AMO, TOM fornece uma maneira de lidar com as funções administrativas como criar modelos, importação e atualização de dados e atribuir funções e permissões.  
  
TOM expõe metadados de tabela nativo, como **modelo**, **tabelas**, **colunas**, e **relações** objetos.  Uma exibição de alto nível da árvore de modelo de objeto, fornecida abaixo, ilustra como as partes do componente estão relacionadas.  
  
 Como TOM é uma extensão do AMO, todas as classes que representam objetos de tabela novo introduzidos no SQL Server 2016 são implementadas em um novo assembly Microsoft.AnalysisServices.Tabular.dll. Classes de uso geral do AMO foram movidos para o assembly de AnalysisServices. Seu código precisa referenciar os dois assemblies.
Consulte [instalar, distribuir e referenciar o modelo de objeto de tabela &#40; AnalysisServices &#41; ](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) para obter detalhes.  
  
 Atualmente, a API está disponível apenas para código gerenciado em .NET framework. Para revisar a lista completa de programação de opções, incluindo o suporte de linguagem de script e de consulta, consulte [programação de modelo de tabela para 1200 de nível de compatibilidade](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md).  
  
## <a name="tabular-object-model-hierarchy"></a>Hierarquia de modelo de objeto de tabela  
 De uma perspectiva lógica, todos os objetos de tabela formam uma árvore, a raiz da qual é um **modelo**, descendente do banco de dados. **Servidor** e **banco de dados** não são considerados "tabular" porque esses objetos também podem representar um banco de dados Multidimensional hospedado em um servidor em execução no modo Multidimensional ou um modelo de tabela de compatibilidade inferior nível que não usam metadados tabulares para definições de objeto. 
  
 Com exceção de **AttributeHierarchy**, **KPI**, e **LinguisticMetadata**, cada objeto filho pode ser um membro de uma coleção. Por exemplo, o **modelo** objeto contém uma coleção de **tabela** objetos (por meio de **tabelas** propriedade), com cada **tabela** objeto que contém uma coleção de **coluna** objetos e assim por diante.  
  
 O descendente de nível mais baixo de qualquer objeto pai dessa hierarquia é uma **anotação** objeto que pode ser usado opcionalmente estender o esquema, desde que você forneça o código para lidar com ele.  
  
 ![diagrama de hierarquia de objeto](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/ssastomobjectmodeldiagram.png "diagrama da hierarquia de objetos")  
  
## <a name="tom-and-other-related-technologies"></a>TOM e outras tecnologias relacionadas

TOM é criado sobre a infraestrutura AMO, que também acomoda Multidimensional e bancos de dados tabulares em níveis de compatibilidade abaixo de 1200.

Isso tem algumas implicações práticas.
Primeiro de tudo, quando você gerencia objetos que não são especificados em metadados de tabela (como uma **servidor** ou **banco de dados**), você precisará aproveitar partes da pilha de AMO existente que descrevem os objetos. Junto com a API herdada é o conceito de objetos principais e secundários que fornecem descrições granulares do estado do objeto como descoberta do servidor, ou quando salvos no servidor. A classe MajorObject no namespace Microsoft. AnalysisServices expõe métodos para **atualizar** e **atualização**. Os objetos menores são somente atualização ou salvo por meio do objeto principal que contém.

Por outro lado, quando você gerencia objetos que fazem parte de metadados de tabela (como **modelo** ou **tabela**), utilize uma pilha de tabela totalmente nova. Dentro esta pilha, o atualizações são refinadas, que significa que todos os objetos de metadados (derivado a **MetadataObject** classe sob o namespace AnalysisServices) podem ser salvos individualmente no servidor. Normalmente, você deve descobrir todo o **modelo**, em seguida, fazer alterações em objetos de metadados individuais nele (como **tabela** ou **coluna**), chame  **Model.SaveChanges()** método (que compreende as alterações feitas por você no nível refinada), enviar comandos ao servidor para atualizar somente os objetos que foram alteradas.

### <a name="tom-and-xmla"></a>TOM e XMLA

Durante a transmissão, TOM usa o protocolo XMLA para se comunicar com o servidor do Analysis Services e para gerenciar objetos. Ao gerenciar objetos não tabulares, TOM usa [ASSL](../scripting/analysis-services-scripting-language-assl-for-xmla.md), a extensão da linguagem de script do Analysis Services do XMLA. Ao gerenciar objetos tabulares, TOM usa o protocolo de tabela do SSAS, também uma extensão do XMLA. Consulte [documentação do protocolo MS-SSAS-T SQL Server Analysis Services Tabular](https://msdn.microsoft.com/library/mt719260.aspx) para obter mais informações.

### <a name="tom-and-json"></a>TOM e JSON

Metadados de tabela, que é estruturado como documentos JSON, tem um novo comando e o objeto de modelo da sintaxe de definição através de linguagem de script de modelo de tabela [TMSL](../tabular-model-scripting-language-tmsl-reference.md). A linguagem de script usa JSON para o corpo de solicitações e respostas.

Embora TMSL e TOM expõem os mesmos objetos (**tabela**, **coluna**, e assim por diante) e as mesmas operações (**criar**, **excluir**,  **Atualizar**), TOM não usa TMSL na conexão (ele usa o protocolo de tabela do SSAS MS em vez disso, conforme observado anteriormente).

Como um usuário, você pode optar por gerenciar bancos de dados tabulares por meio da biblioteca de TOM do seu programa em c# ou o script do PowerShell ou por meio de script TMSL executadas por meio do PowerShell, um trabalho do SQL Server Agent ou o SQL Server Management Studio (SSMS).

A decisão de usar um ou outro ficará às especificações de seus requisitos. A biblioteca de TOM fornece maior funcionalidade em comparação comparada TMSL. Especificamente, ao passo que o TMSL oferece apenas operações de alta granularidade no nível do banco de dados, tabela, partição ou função, TOM permite operações muito mais individualizadas. Para gerar ou atualizar modelos programaticamente, você precisará toda a extensão da API na biblioteca de TOM.
  
## <a name="see-also"></a>Consulte também  
 [Programação de modelo de tabela para o nível de compatibilidade 1200](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
[O Analysis Services PowerShell](../../analysis-services/powershell/analysis-services-powershell-reference.md)
  

