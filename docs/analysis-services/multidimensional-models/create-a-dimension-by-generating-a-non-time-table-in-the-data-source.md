---
title: "Criar uma dimensão ao gerar uma tabela não seja de tempo na fonte de dados | Microsoft Docs"
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
- data sources [Analysis Services], dimensions without data source
- dimensions [Analysis Services], standard
- dimensions [Analysis Services], creating without data source
- standard dimensions [Analysis Services]
ms.assetid: a37f7a46-7451-4582-ba19-2595196d97bc
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 20035f6d8fff0c5d45b4c807cf6202531156741d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-dimension-by-generating-a-non-time-table-in-the-data-source"></a>Criar uma dimensão ao gerar uma tabela que não seja de tempo na fonte de dados
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar o Assistente para Dimensões no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para criar uma dimensão sem usar uma fonte de dados existente. Isso é possível selecionando a opção **Gerar uma tabela que não seja de tempo na fonte de dados** da página **Selecionar Método de Criação** do assistente. Para criar uma nova tabela de dimensão na fonte de dados subjacente, você precisa ter permissão para criar objetos na fonte de dados subjacente. Ao definir uma dimensão sem uma exibição da fonte de dados predefinida, você pode definir a dimensão do zero ou pode usar um modelo de dimensão.  
  
 O Assistente para Dimensões fornece modelos de dimensão de exemplo, com os quais é possível construir um tipo de dimensão comum. Você pode selecionar a partir dos seguintes tipos de dimensão:  
  
-   Conta  
  
-   Cliente  
  
-   Data  
  
-   Departamento  
  
-   Moeda de destino  
  
-   Employee  
  
-   Geografia  
  
-   Detalhes do pedido de vendas pela Internet  
  
-   Organização  
  
-   Product  
  
-   Promoção  
  
-   Detalhes do pedido de vendas do revendedor  
  
-   Reseller  
  
-   Canal de vendas  
  
-   Motivo de vendas  
  
-   Detalhes do resumo do pedido de vendas  
  
-   Sales Territory  
  
-   Cenário  
  
-   Moeda de origem  
  
 Cada um dos modelos padrão dá suporte a atributos que você pode escolher para serem incluídos na dimensão. Você também pode adicionar seus próprios arquivos de modelo a dimensões que geralmente são usadas com seus dados. Os modelos de dimensão ficam na seguinte pasta:  
  
 `C:\Program Files\Microsoft SQL Server\100\Tools\Templates\olap\1033\Dimension Templates`  
  
 Você pode usar o Designer de Dimensão depois de concluir o Assistente para Dimensões para adicionar, remover, e configurar atributos e hierarquias na dimensão.  
  
 Quando você estiver criando uma dimensão que não seja de tempo sem usar uma fonte de dados, o Assistente para Dimensões o orientará durante as etapas de especificação do tipo de dimensão, identificando o atributo de chave, com dimensão de alteração lenta.  
  
## <a name="specify-dimension-type"></a>Especificar tipo de dimensão  
 Na página **Especificar Tipo de Dimensão** do Assistente para Dimensões, você pode especificar o tipo de dimensão. Se você estiver criando a dimensão com base em um modelo, o tipo de dimensão será definido para você. Nessa página, você também pode selecionar atributos padrão para o tipo de dimensão especificado, se houver algum disponível.  
  
 Se você selecionou um modelo que corresponde a um tipo de dimensão, essa página será populada com as opções do tipo de dimensão em questão. Se você não selecionar um modelo, ou se não houver nenhum tipo de dimensão correspondente, o tipo de dimensão padrão será **Regular**. Se um tipo de dimensão não estiver selecionado, selecione o tipo mais apropriado para a dimensão que você está criando. Se nenhum tipo apropriado estiver listado para **Tipo de dimensão**, use **Regular**.  
  
 Quando você seleciona um tipo de dimensão, o assistente lista os tipos de atributo que se aplicam a esta dimensão em **Atributos de dimensão**. Para selecionar um tipo de atributo, marque a caixa de seleção **Incluir** próximo ao tipo de atributo e digite o nome para o atributo em **Atributo de Dimensão**. O nome padrão é igual ao **Tipo de Atributo**.  
  
## <a name="identify-key-attribute-and-changing-dimensions"></a>Identificar Atributo de Chave e dimensões variáveis  
 Na página **Especificar Chave e Tipo de Dimensão** , selecione o atributo que você quer que seja o atributo de chave para a dimensão. O atributo de chave corresponde normalmente à coluna de chave primária na tabela principal de dimensão e normalmente cria índices dos membros folha da dimensão.  
  
 Se você selecionou um modelo, e um atributo de chave está definido no modelo, esse atributo será o atributo de chave padrão. Se você selecionou um modelo, mas nenhum atributo de chave está definido no modelo, o padrão será o primeiro atributo da lista. A lista contém todos os atributos que você selecionou na página **Especificar Tipo de Dimensão** . Você pode selecionar qualquer um dos atributos selecionados na página **Especificar Tipo de Dimensão** para ser o atributo de chave. Se você não selecionou nenhum atributo, o assistente criará um atributo de chave automaticamente e o nomeará concatenando o nome e a ID da dimensão.  
  
 Finalmente, especifique se essa dimensão é uma dimensão variável. Com o tempo, membros em uma dimensão variável são movidos com o tempo para locais diferentes na hierarquia. O assistente gera colunas adicionais e cria atributos que correspondem a essas colunas. Essas colunas permitirão que os usuários consultem a dimensão de forma a influenciar na alteração. Qualquer pacote que for criado depois com o Assistente de Geração de Esquema vai gerenciar chaves substitutas com base em características de dimensão de alteração lenta da dimensão.  
  
 Quando você marcar a caixa de seleção **Esta é uma dimensão variável** , o Assistente para Dimensões definirá os atributos indicados na seguinte tabela:  
  
|Atributo|Tipo|  
|---------------|----------|  
|SCD OriginalID|SCDOriginalID|  
|Data de Término da SCD|SCDEndDate|  
|Data de Início da SCD|SCDStartDate|  
|Status da SCD|SCDStatus|  
  
 Por padrão, a caixa de seleção **Esta é uma dimensão variável** ficará marcada se você usar um modelo que tenha esses atributos de dimensão de alteração lenta definidos. Se você desmarcar a caixa de seleção, os atributos de dimensão de alteração lenta serão removidos da dimensão.  
  
 Você pode usar o Designer de Dimensão para configurar as propriedades para uma dimensão de alteração lenta.  
  
## <a name="completing-the-dimension-wizard"></a>Concluindo o Assistente para Dimensões  
 Na página **Concluindo o Assistente** , digite um nome para a nova dimensão e veja a estrutura da dimensão. Marque a caixa de seleção **Gerar esquema agora** para iniciar o Assistente de Geração de Esquema depois que você clicar em **Concluir**. Na maioria dos casos, você não deve marcar esta caixa de seleção se planejar criar outros objetos. Se você não marcar essa caixa de seleção, poderá usar o Designer de Dimensão para gerar o esquema posteriormente.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma dimensão de tempo ao gerar uma tabela de tempo](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Criar uma dimensão de tempo ao gerar uma tabela de tempo](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)  
  
  

