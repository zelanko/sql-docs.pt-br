---
title: Traduções em modelos multidimensionais (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ac278f3e254e353d9ab7b6dc6d6fd7850b442c9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="translations-in-multidimensional-models-analysis-services"></a>Traduções em modelos multidimensionais (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Você pode definir traduções no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o designer apropriado para o objeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que será traduzido. Definir uma tradução cria um objeto **Translation** associado ao objeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] apropriado que tenha os valores literais explícitos especificados, no idioma especificado, para as propriedades do objeto associado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>Elementos de um modelo de dados em vários idiomas  
 Um modelo de dados usado em uma solução em vários idiomas precisa de mais do que rótulos (nomes de campo e descrições) traduzidos. Ele também precisa fornecer valores de dados que são articulados em vários scripts de idioma. Para obter uma solução em vários idiomas é necessário que você tenha atributos individuais, associado a colunas em um banco de dados externo que retorna os dados.  
  
 Os bancos de dados de exemplo da Adventure Works (multidimensional, bem como o data warehouse relacional) demonstram as funcionalidades de tradução do Analysis Services. O modelo de exemplo inclui descrições e legendas traduzidas. O data warehouse relacional de exemplo contém colunas de valores traduzidos que fornecem membros de atributo traduzidos no modelo.  
  
 Para exibir valores de dados convertidos disponíveis para o modelo:  
  
1.  Abra o modelo multidimensional da Adventure Works no designer.  
  
2.  No Gerenciador de soluções, abra exibições da fonte de dados e clique duas vezes em Adventure Works DW\<versão >. DSV.  
  
3.  Encontre dimDate, dimProduct, dimProductCategory ou dimProductSubcateogry. Todas essas dimensões contêm atributos para membros traduzidos para o mês, dia da semana, nome do produto, nome da categoria e assim por diante.  
  
4.  Clique com o botão direito do mouse em qualquer campo e selecione **Explorar dados**. Você verá as traduções em francês, espanhol e inglês de cada membro.  
  
 Formatos de data, hora e moeda não são implementados por meio de traduções. Para fornecer dinamicamente formatos culturalmente específicos com base na localidade do cliente, use o Assistente de conversão de moeda e a propriedade **FormatString** . Consulte [Conversões de moeda e &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md) e [Elemento FormatString &#40;ASSL&#41;](../../analysis-services/scripting/properties/formatstring-element-assl.md) para obter detalhes.  
  
 [Lesson 9: Defining Perspectives and Translations](../../analysis-services/lesson-9-defining-perspectives-and-translations.md) no Tutorial do Analysis Services orientará você pelas etapas de criação e teste de traduções.  
  
## <a name="defining-translations"></a>Definindo traduções  
  
### <a name="add-translations-to-a-cube"></a>Adicionar traduções a um cubo  
 Você pode adicionar traduções ao cubo, grupos de medidas, medidas, dimensões do cubo, perspectivas, KPIs, ações, conjuntos nomeados e membros calculados.  
  
1.  No Gerenciador de Soluções, clique duas vezes no nome do cubo para abrir o designer de cubo.  
  
2.  Clique na guia **Conversões** . Todos os objetos que dão suporte a traduções estão listados nesta página.  
  
3.  Para cada objeto, especifique o idioma de destino (resolve internamente para um LCID), legenda traduzida e descrição traduzida. A lista de idiomas é consistente em todo o Analysis Services, se você estiver definindo o idioma do servidor no Management Studio ou adicionando uma substituição de tradução em um único atributo.  
  
     Lembre-se de que você não pode alterar o agrupamento. Um cubo essencialmente usa um agrupamento, mesmo se você estiver dando suporte a vários idiomas por meio de legendas traduzidas (há uma exceção para atributos de dimensão, discutida abaixo). Se os idiomas não forem classificados corretamente no agrupamento compartilhado, será necessário fazer cópias do cubo para acomodar seus requisitos de agrupamento.  
  
4.  Compilar e implantar o projeto.  
  
5.  Conecte-se ao banco de dados usando um aplicativo cliente, como o Excel, modificando a cadeia de conexão para usar o identificador de localidade. Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md) para obter detalhes.  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Adicionar traduções a uma dimensão e atributos  
 Você pode adicionar traduções a dimensões de banco de dados, atributos, hierarquias e níveis em uma hierarquia.  
  
 Legendas traduzidas são adicionadas ao modelo manualmente usando o teclado ou copiar e colar, mas para membros de atributo de dimensão, você pode obter valores traduzidos de um banco de dados externo. Especificamente, a propriedade **CaptionColumn** de um atributo pode ser associada a uma coluna em uma exibição da fonte de dados.  
  
 No nível de atributo, você pode substituir as configurações de agrupamento, por exemplo, você pode desejar ajustar diferenciação de largura ou usar uma classificação binária para um atributo específico. Em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o agrupamento é exposto onde as associações de dados são definidas. Como você está associando uma tradução de atributo de dimensão a uma coluna de origem diferente no DSV, uma configuração de agrupamento está disponível para que você possa especificar o agrupamento usado pela coluna de origem. Consulte [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) para obter detalhes sobre o agrupamento da coluna no banco de dados relacional.  
  
1.  No Gerenciador de Soluções, clique duas vezes no nome da dimensão para abrir o designer de dimensão.  
  
2.  Clique na guia **Conversões** . Todos os objetos de dimensão que dão suporte a traduções estão listados nesta página.  
  
     Para cada objeto, especifique o idioma de destino (resolve para um LCID), legenda traduzida e descrição traduzida. A lista de idiomas é consistente em todo o Analysis Services, se você estiver definindo o idioma do servidor no Management Studio ou adicionando uma substituição de tradução em um único atributo.  
  
3.  Para associar um atributo a uma coluna fornecendo valores traduzidos:  
  
    1.  Ainda em Designer de dimensão | **Translações**, adicione uma nova translação. Escolha o idioma. Uma nova coluna é exibida na página para aceitar os valores traduzidos.  
  
    2.  Coloque o cursor em uma célula vazia adjacente a um dos atributos. O atributo não pode ser a chave, mas todos os outros atributos são opções viáveis. Você verá um pequeno botão com um ponto dentro. Clique no botão para abrir a **Caixa de diálogo de tradução de dados do atributo**.  
  
    3.  Inserir uma tradução para a legenda. Isso é usado como um rótulo de dados no idioma de destino, por exemplo, como um nome de campo em uma lista de campos da tabela dinâmica.  
  
    4.  Escolha a coluna de origem que fornece os valores de membros de atributo traduzidos. Somente colunas já existentes na tabela ou consulta associada à dimensão estão disponíveis. Se a coluna não existir, você precisa modificar a exibição da fonte de dados, dimensão e cubo para selecionar a coluna.  
  
    5.  Escolha a ordem de agrupamento e de classificação, se aplicável.  
  
4.  Compilar e implantar o projeto.  
  
5.  Conecte-se ao banco de dados usando um aplicativo cliente, como o Excel, modificando a cadeia de conexão para usar o identificador de localidade. Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md) para obter detalhes.  
  
### <a name="add-a-translation-of-the-database-name"></a>Adicionar uma tradução do nome do banco de dados  
 No nível do banco de dados, você pode adicionar traduções para o nome do banco de dados e descrição. O nome do banco de dados traduzido pode estar visível nas conexões de cliente que especificam o LCID do idioma, mas que depende da ferramenta. Por exemplo, exibir o banco de dados no Management Studio não mostrará o nome traduzido, mesmo que você especifique o identificador de localidade na conexão. A API usada pelo Management Studio para se conectar ao Analysis Services não lê a propriedade **Language** .  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no nome do projeto | **Editar banco de dados** para abrir o designer de banco de dados.  
  
2.  Em Traduções, especifique o idioma de destino (resolve para um LCID), legenda traduzida e descrição traduzida. A lista de idiomas é consistente em todo o Analysis Services, quer você esteja definindo o idioma do servidor no Management Studio ou adicionando uma substituição de tradução em um único atributo.  
  
3.  Na página Propriedades do banco de dados, defina **Language** com o mesmo LCID especificado para a tradução. Opcionalmente, defina **Collation** também se o padrão não fizer mais sentido.  
  
4.  Compilar e implantar o banco de dados.  
  
## <a name="deleting-translation-objects"></a>Excluindo objetos de tradução  
 Você pode clicar com o botão direito em um objeto de tradução na dimensão ou designer de cubo para removê-lo permanentemente. Você não pode restaurar nem reciclar um objeto excluído, portanto, examine a lista de objetos afetados antes de continuar.  
  
## <a name="resolving-translations"></a>Resolvendo traduções  
 Se um aplicativo cliente solicita informações em um identificador de idioma específico, a instância no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta resolver dados e metadados para objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o identificador de idioma mais próximo possível. Se o aplicativo cliente não especificar um idioma padrão, especificar o identificador de localidade neutro (0) ou identificador de idioma padrão (1024), o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o idioma padrão para a instância para retornar dados e metadados para objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se um aplicativo cliente especifica um identificador de idioma diferente do identificador de idioma padrão, a instância itera por meio das traduções disponíveis para todos os objetos disponíveis. Se o identificador de idioma especificado corresponder ao identificador de idioma de uma tradução, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retornará essa tradução. Se uma correspondência não puder ser encontrada, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará usar um dos seguintes métodos para retornar traduções com o identificador de idioma que seja mais próximo do identificador do idioma especificado.  
  
-   Para os seguintes identificadores de idioma, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará usar um identificador de idioma alternativo se a tradução para o identificador de idioma especificado não for definido:  
  
    |Identificador de idioma especificado|Identificador de linguagem alternativo|  
    |-----------------------------------|-----------------------------------|  
    |3076 - Chinês (Hong Kong SAR, PRC)|1028 - Chinês (Taiwan)|  
    |5124 - Chinês (Macau SAR)|1028 - Chinês (Taiwan)|  
    |1028 - Chinês (Taiwan)|Idioma padrão|  
    |4100 – Chinês (Singapura)|2052 - Chinês (PRC)|  
    |2074 - Croata|Idioma padrão|  
    |3098 - Croata (Cirílico)|Idioma padrão|  
  
-   Para todos os outros identificadores de idioma especificados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] extrai o idioma principal do identificador de idioma especificado e recupera o identificador de idioma indicado pelo Windows como a melhor correspondência para o idioma principal. Se uma tradução para a melhor correspondência de identificador de idioma não puder ser encontrada ou se o identificador de idioma especificado for a melhor correspondência para o idioma principal, então, o idioma padrão será usado.  
  
## <a name="see-also"></a>Consulte também  
 [Cenários de globalização para o Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Idiomas e agrupamentos &#40;do Analysis Services&#41;](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
