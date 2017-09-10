---
title: "Ações (Analysis Services - dados multidimensionais) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- actions [Analysis Services]
- actions [Analysis Services], about actions
- MDX [Analysis Services], actions
- cubes [Analysis Services], actions
- OLAP objects [Analysis Services], actions
ms.assetid: 07229bb2-805c-427e-8455-69c9ca5d01e0
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a61563367d64f9122441991d125cf987f6ddc4d6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="actions-analysis-services---multidimensional-data"></a>Ações (Analysis Services – Dados Multidimensionais)
  As ações podem ser de tipos diferentes e devem ser criadas adequadamente. As ações podem ser:  
  
-   Ações de detalhamento, que retornam o conjunto de linhas que representa os dados subjacentes das células selecionadas do cubo onde a ação ocorre.  
  
-   Ações de relatório, que retornam um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] associado a uma seção selecionada do cubo onde a ação ocorre.  
  
-   Ações padrão, que retornam o elemento de ação (URL, HTML, DataSet, RowSet e outros elementos) associado a uma seção selecionada do cubo onde a ação ocorre.  
  
 Uma interface de consulta, como ADOMD.NET, é usada pelo aplicativo cliente para recuperar e expor as ações ao usuário final. Para obter mais informações, consulte [Desenvolvendo com ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.Action> é composto de: informações básicas, o destino no qual a ação deve ocorrer, uma condição para limitar o escopo da ação e o tipo. As informações básicas incluem o nome da ação, sua descrição, a legenda sugerida e outros.  
  
 O destino é o local real no cubo onde a ação deve acontecer. O destino é composto de um tipo de destino e um objeto de destino. O tipo de destino representa o tipo de objeto, no cubo, onde a ação será habilitada. Tipo de destino pode ser membros de nível, células, hierarquia, membros de hierarquia ou outros. O objeto de destino for um objeto específico do tipo de destino, se o tipo de destino for hierarquia, então o objeto de destino será qualquer uma das hierarquias definidas no cubo.  
  
 A condição é uma expressão MDX **Boolean** avaliada no evento da ação. Se a condição for avaliada como **true**, então, a ação será executada. Caso contrário, a ação não será executada.  
  
 O tipo é a forma de ação a ser executada. <xref:Microsoft.AnalysisServices.Action> é uma classe abstrata, portanto, a ser usada se precisar usar uma das classes derivadas. Dois tipos de ações são predefinidos: análise e relatório. Elas têm classes derivadas correspondentes: <xref:Microsoft.AnalysisServices.DrillThroughAction> e <xref:Microsoft.AnalysisServices.ReportAction>. Outras ações são abrangidas na classe <xref:Microsoft.AnalysisServices.StandardAction> .  
  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma ação é uma instrução MDX armazenada que pode ser apresentada e implantada por aplicativos cliente. Em outras palavras, uma ação é um comando cliente definido e armazenado no servidor. Uma ação também contém informações que especificam quando e como uma instrução MDX deve ser exibida e tratada pelo aplicativo cliente. A operação especificada pela ação pode iniciar um aplicativo, usando as informações na ação como um parâmetro ou pode recuperar informações com base em critérios fornecidos pela ação.  
  
 As ações permitem que usuários empresariais ajam nos resultados de suas análises. Salvando e reusando ações, os usuários finais podem ir além da análise tradicional, que geralmente termina com a apresentação de dados e inicia soluções para problemas e deficiências descobertas, estendendo assim os aplicativos de business intelligence além do cubo. As ações podem transformar o aplicativo cliente de uma ferramenta de renderização de dados sofisticada em parte integral do sistema operacional da empresa. Em vez de focalizar os dados de envio como entrada de aplicativos operacionais, os usuários finais "fecham o ciclo" do processo de tomada de decisões. Essa capacidade de transformar dados analíticos em decisões é crucial para o sucesso do aplicativo Business Intelligence.  
  
 Por exemplo, um usuário empresarial que navega em um cubo observa que o estoque atual de um determinado produto está baixo. O aplicativo cliente fornece ao usuário empresarial uma lista de ações, todas relacionadas ao valor de baixo estoque do produto, recuperadas do banco de dados do Analysis Services; o usuário empresarial selecionar a ação Pedido para o membro do cubo que representa o produto. A ação Pedido inicia um novo pedido chamando o procedimento armazenado no banco de dados operacional. Esse procedimento armazenado gera as informações apropriadas para enviar a serem enviadas ao sistema de entrada de pedidos.  
  
 Há flexibilidade na criação de ações: por exemplo, uma ação pode iniciar um aplicativo ou recuperar informações do banco de dados. Você pode configurar uma ação a ser disparada de praticamente qualquer parte de um cubo, incluindo dimensões, níveis, membros e células ou criar várias ações para a mesma parte de um cubo. Você também pode passar parâmetros de cadeia de caracteres para os aplicativos iniciados e especificar as legendas exibidas aos usuários finais à medida que a ação é executada.  
  
> [!IMPORTANT]  
>  Para que um usuário empresarial use as ações, o aplicativo cliente empregado pelo usuário empresarial deve oferecer suporte a ações.  
  
## <a name="types-of-actions"></a>Tipos de ações  
 A tabela a seguir lista os tipos de ações incluídos em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|Tipo de ação|Description|  
|-----------------|-----------------|  
|CommandLine|Executa um comando no prompt de comando.|  
|Conjunto de dados|Retorna um conjunto de dados a um aplicativo cliente.|  
|Detalhamento|Retorna uma instrução de detalhamento como uma expressão e que o cliente executa para retornar um conjunto de dados.|  
|Html|Executa um script HTML em um navegador de Internet.|  
|Proprietário|Executa uma operação usando uma interface diferente das listadas nesta tabela.|  
|Relatório|Envia uma solicitação com base em URL parametrizada para um servidor de relatórios e retorna um relatório a um aplicativo cliente.|  
|Conjunto de linhas|Retorna um conjunto de linhas a um aplicativo cliente.|  
|Instrução|Executa um comando OLE DB.|  
|URL|Exibe uma página da Web dinâmica em um navegador de Internet.|  
  
## <a name="resolving-and-executing-actions"></a>Resolvendo e executando ações  
 Quando um usuário empresarial acessa o objeto pra o qual o objeto de comando está definido, a instrução associada à ação é automaticamente resolvida, o que o torna disponível para o aplicativo cliente, mas a ação não é executada automaticamente. A ação só é executada quando o usuário empresarial executar a operação específica ao cliente que inicia a ação. Por exemplo, um aplicativo cliente pode exibir uma lista de ações como menu pop-up, quando o usuário empresarial clica com o botão direito do mouse em um membro ou célula em particular.  
  
## <a name="see-also"></a>Consulte também  
 [Ações em modelos multidimensionais](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
  
