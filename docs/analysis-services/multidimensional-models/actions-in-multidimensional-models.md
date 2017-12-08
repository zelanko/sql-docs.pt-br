---
title: "Ações em modelos multidimensionais | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services], creating
- report actions [Analysis Services]
- drillthrough actions [Analysis Services]
- cubes [Analysis Services], actions
ms.assetid: b9fee2b9-05a5-4077-848d-d8457326dc27
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ce19f2ad400f0a3e01efae5fea89235905025414
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="actions-in-multidimensional-models"></a>Ações em modelos multidimensionais
  Uma ação é uma operação iniciada pelo usuário final em um cubo selecionado ou em parte de um cubo. A operação pode iniciar um aplicativo com o item selecionado como parâmetro ou pode recuperar informações sobre o item selecionado. Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 Use a guia **Ações** do Designer de Cubo para criar ações para um cubo. Especifique o seguinte:  
  
 **Nome**  
 Selecione um nome que identifica a ação.  
  
 **Destino da Ação**  
 Selecione o objeto ao qual a ação será anexada. Em geral, em aplicativos cliente, a ação é exibida quando os usuários finais selecionam o objeto de destino; no entanto, o aplicativo cliente determina qual operação do usuário final exibe ações. Para **Tipo de destino**, selecione entre os objetos a seguir:  
  
-   Membros de atributo  
  
-   Células  
  
-   Cube  
  
-   Membros de dimensão  
  
-   Hierarquia  
  
-   Membros de hierarquia  
  
-   Nível  
  
-   Membros de nível  
  
 Depois de selecionar o tipo de objeto de destino, em **Objeto de destino**, selecione o objeto de cubo do tipo designado.  
  
 **Condição (Opcional)**  
 Especifique uma expressão MDX opcional que resolve um valor booliano. Se o valor for **True**, a ação será executada no destino especificado. Se for **False**, a ação não será executada.  
  
 **Conteúdo da Ação**  
 Selecione o tipo de ação. A tabela a seguir resume os tipos disponíveis:  
  
|Tipo|Description|  
|----------|-----------------|  
|Conjunto de Dados|Recupera um conjunto de dados.|  
|Proprietário|Executa uma operação usando uma interface diferente das listadas nesta tabela.|  
|Conjunto de Linhas|Recupera um conjunto de linhas.|  
|Instrução|Executa um comando OLE DB.|  
|URL|Exibe uma página variável em um navegador de Internet.|  
  
 Para **Expressão da Ação**, especifique os parâmetros que são passados quando a ação é executada. A sintaxe deve avaliar uma cadeia de caracteres e você deve incluir uma expressão escrita em MDX. Por exemplo, a expressão MDX pode indicar uma parte do cubo incluída na sintaxe. Expressões MDX são avaliadas antes de os parâmetros serem passados. Além disso, o Construtor MDX está disponível para lhe ajudar a construir expressões MDX.  
  
 **Propriedades Adicionais**  
 Selecione a propriedade. A tabela a seguir resume as propriedades disponíveis:  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Invocação**|Especifica como a ação é executada. Interativo, o padrão, especifica que a ação será executada quando um usuário acessar um objeto. Os configurações possíveis são:<br /><br /> Lote<br /><br /> Interativo<br /><br /> Em Aberto|  
|**Aplicativo**|Descreve o aplicativo da ação.|  
|**Description**|Descreve a ação.|  
|**Caption**|Fornece uma legenda que é exibida para a ação. Se a legenda for MDX, especifique **True** para **A legenda é MDX**.|  
|**A legenda é MDX**|Especifique **True** se a legenda for MDX ou **False** se não for.|  
  
> [!NOTE]  
>  Use o Analysis Services Scripting Language (ASSL) ou o Objetos de Gerenciamento de Análise (AMO) para definir tipos de ação HTML ou de linha de comando. Para obter mais informações, consulte [Elemento Action &#40;ASSL&#41;](../../analysis-services/scripting/objects/action-element-assl.md), [Elemento Type &#40;Ação&#41; &#40;ASSL&#41;](../../analysis-services/scripting/properties/type-element-action-assl.md) e [Programando objetos OLAP AMO avançados](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md).  
  
## <a name="creating-a-reporting-action"></a>Criando uma ação de relatório  
 O servidor de relatório responde a solicitações baseadas na URL para relatórios. Para criar uma ação de relatório, no menu **Cubo** , clique em **Nova Ação de Relatório**. As opções a seguir são específicas de uma ação de relatório.  
  
 **Servidor de relatório**  
 As propriedades descritas na tabela a seguir são especificadas para o servidor de relatório.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Nome do servidor**|O nome do computador que executa o servidor de relatório.|  
|**Caminho do servidor**|O caminho exibido pelo servidor de relatório.|  
|**Formato do relatório**|HTML5, HTML3, Excel ou PDF.|  
  
> [!NOTE]  
>  Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você pode especificar a Segurança da Camada de Transporte (https:) na propriedade de nome do servidor.  
  
 **Parâmetros (Opcional)**  
 Os parâmetros serão enviados ao servidor como parte da cadeia de caracteres de URL quando a ação for criada. Incluem **Nome do Parâmetro** e **Valor do Parâmetro**, que são uma expressão MDX.  
  
 A URL do servidor de relatório é construída da seguinte maneira:  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 Por exemplo:  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>Criando um ação de detalhamento  
 Uma ação de extração de detalhes é definida por uma ação de conjunto de linhas, retornada ao aplicativo cliente como uma instrução de extração de detalhes. O destino de ação é um membro de um grupo de medidas. Para criar uma nova ação de drillthrough, no menu **Cubo** , clique em **Nova Ação de Drillthrough**. As opções a seguir são específicas de uma ação de extração de detalhes:  
  
 **Colunas de Extração de Detalhes**  
 Selecione uma ou mais dimensões e, para cada uma, as colunas de detalhamento retornadas ao aplicativo cliente pela ação.  
  
## <a name="see-also"></a>Consulte também  
 [Cubos em modelos multidimensionais](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
