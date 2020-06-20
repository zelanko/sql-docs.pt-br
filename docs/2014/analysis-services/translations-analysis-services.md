---
title: Traduções (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7417efef16ae16ef11b955af12ba8dbbd549939c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938317"
---
# <a name="translations-analysis-services"></a>Traduções (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]** Somente multidimensional  
  
 Em um modelo de dados multidimensionais [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , você pode inserir várias traduções de uma legenda para fornecer sequências de caracteres específicas da localidade com base no LCID. As traduções podem ser adicionadas para o nome do banco de dados, objetos de cubo e objetos de dimensão do banco de dados.  
  
 A definição de uma tradução cria os metadados e a legenda traduzida dentro do modelo, mas para renderizar cadeias de caracteres localizadas em um aplicativo cliente, você deve definir a propriedade `Language` no objeto ou passar um parâmetro `Locale Identifier` na cadeia de conexão (por exemplo, definindo `LocaleIdentifier=1036` para retornar cadeias de caracteres em francês). Planeje o uso de `Locale Identifier` para dar suporte a várias traduções simultâneas do mesmo objeto em idiomas diferentes. Definir a propriedade `Language` funciona, mas isso também afeta o processamento e as consultas, o que pode ter consequências indesejadas. Definir `Locale Identifier` é a melhor opção porque ele é usado somente para retornar cadeias de caracteres traduzidas.  
  
 Uma tradução consiste em um identificador de localidade (LCID), uma legenda traduzida para o objeto (por exemplo, a dimensão ou o nome do atributo) e, opcionalmente, uma associação a uma coluna que fornece valores de dados no idioma de destino. Você pode ter várias traduções, mas só pode usar uma para determinada conexão. Não há nenhum limite teórico no número de traduções que você pode inserir no modelo, mas cada tradução adiciona complexidade ao teste e todas as traduções devem compartilhar a mesma ordenação, portanto, ao criar a solução, lembre-se dessas restrições naturais.  
  
> [!TIP]  
>  Você pode usar os aplicativos cliente, como o Excel, o Management Studio e o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para retornar cadeias de caracteres traduzidas. Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) para obter detalhes.  
  
## <a name="setting-up-a-model-to-support-translated-members"></a>Configuração de um modelo para dar suporte a membros traduzidos  
 Um modelo de dados usado em uma solução em vários idiomas precisa de mais do que rótulos (nomes de campo e descrições) traduzidos. Ele também precisa fornecer valores de dados que são articulados em vários scripts de idioma. Para obter uma solução em vários idiomas é necessário que você tenha atributos individuais, associado a colunas em um banco de dados externo que retorna os dados.  
  
 Os bancos de dados de exemplo da Adventure Works (multidimensional, bem como o data warehouse relacional) demonstram o recurso de tradução. O modelo de exemplo inclui descrições e legendas traduzidas. O data warehouse relacional de exemplo contém colunas de valores traduzidos que fornecem membros de atributo traduzidos no modelo.  
  
 Para exibir valores de dados convertidos disponíveis para o modelo:  
  
1.  Abra o modelo multidimensional da Adventure Works no designer.  
  
2.  Em Gerenciador de Soluções, abra exibições da fonte de dados e clique duas vezes em Adventure Works DW \<version> . DSV.  
  
3.  Encontre dimDate, dimProduct, dimProductCategory ou dimProductSubcateogry. Todas essas dimensões contêm atributos para membros traduzidos para o mês, dia da semana, nome do produto, nome da categoria e assim por diante.  
  
4.  Clique com o botão direito do mouse em qualquer campo e selecione **Explorar dados**. Você verá as traduções em francês, espanhol e inglês de cada membro.  
  
 Formatos de data, hora e moeda não são implementados por meio de traduções. Para fornecer dinamicamente formatos culturalmente específicos com base na localidade do cliente, use o Assistente de Conversão de Moeda e a propriedade `FormatString`. Consulte [Conversões de moeda e &#40;Analysis Services&#41;](currency-conversions-analysis-services.md) e [Elemento FormatString &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl) para obter detalhes.  
  
 [Lesson 9: Defining Perspectives and Translations](lesson-9-defining-perspectives-and-translations.md) no Tutorial do Analysis Services orientará você pelas etapas de criação e teste de traduções.  
  
## <a name="defining-translations"></a>Definindo traduções  
 A definição de uma tradução cria um objeto `Translation` como um filho de banco de dados, dimensão ou cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Use [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] para abrir a solução e definir traduções.  
  
### <a name="add-translations-to-a-cube"></a>Adicionar traduções a um cubo  
 Você pode adicionar traduções ao cubo, grupos de medidas, medidas, dimensões do cubo, perspectivas, KPIs, ações, conjuntos nomeados e membros calculados.  
  
1.  No Gerenciador de Soluções, clique duas vezes no nome do cubo para abrir o designer de cubo.  
  
2.  Clique na guia **traduções** . Todos os objetos que dão suporte a traduções são listados nesta página.  
  
3.  Para cada objeto, especifique o idioma de destino (resolve internamente para um LCID), legenda traduzida e descrição traduzida. A lista de idiomas é consistente em todo o Analysis Services, se você estiver definindo o idioma do servidor no Management Studio ou adicionando uma substituição de tradução em um único atributo.  
  
     Lembre-se de que você não pode alterar a ordenação. Um cubo essencialmente usa uma ordenação, mesmo se você estiver dando suporte a vários idiomas por meio de legendas traduzidas (há uma exceção para atributos de dimensão, discutida abaixo). Se os idiomas não forem classificados corretamente na ordenação compartilhada, será necessário fazer cópias do cubo para acomodar seus requisitos de ordenação.  
  
4.  Compilar e implantar o projeto.  
  
5.  Conecte-se ao banco de dados usando um aplicativo cliente, como o Excel, modificando a cadeia de conexão para usar o identificador de localidade. Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) para obter detalhes.  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Adicionar traduções a uma dimensão e atributos  
 Você pode adicionar traduções a dimensões de banco de dados, atributos, hierarquias e níveis em uma hierarquia.  
  
 Legendas traduzidas são adicionadas ao modelo manualmente usando o teclado ou copiar e colar, mas para membros de atributo de dimensão, você pode obter valores traduzidos de um banco de dados externo. Especificamente, a propriedade `CaptionColumn` de um atributo pode ser associada a uma coluna em uma exibição da fonte de dados.  
  
 No nível de atributo, você pode substituir as configurações de ordenação, por exemplo, você pode desejar ajustar diferenciação de largura ou usar uma classificação binária para um atributo específico. Em [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a ordenação é exposta onde as associações de dados são definidas. Como você está associando uma tradução de atributo de dimensão a uma coluna de origem diferente no DSV, uma configuração de ordenação está disponível para que você possa especificar a ordenação usada pela coluna de origem. Consulte [Definir ou alterar a ordenação de coluna](../relational-databases/collations/set-or-change-the-column-collation.md) para obter detalhes sobre a ordenação da coluna no banco de dados relacional.  
  
1.  No Gerenciador de Soluções, clique duas vezes no nome da dimensão para abrir o designer de dimensão.  
  
2.  Clique na guia **traduções** . Todos os objetos de dimensão que dão suporte a conversões são listados nesta página.  
  
     Para cada objeto, especifique o idioma de destino (resolve para um LCID), legenda traduzida e descrição traduzida. A lista de idiomas é consistente em todo o Analysis Services, se você estiver definindo o idioma do servidor no Management Studio ou adicionando uma substituição de tradução em um único atributo.  
  
3.  Para associar um atributo a uma coluna fornecendo valores traduzidos:  
  
    1.  Ainda em Designer de dimensão | **Translações**, adicione uma nova translação. Escolha o idioma. Uma nova coluna é exibida na página para aceitar os valores traduzidos.  
  
    2.  Coloque o cursor em uma célula vazia adjacente a um dos atributos. O atributo não pode ser a chave, mas todos os outros atributos são opções viáveis. Você verá um pequeno botão com um ponto dentro. Clique no botão para abrir a **Caixa de diálogo de tradução de dados do atributo**.  
  
    3.  Inserir uma tradução para a legenda. Isso é usado como um rótulo de dados no idioma de destino, por exemplo, como um nome de campo em uma lista de campos da tabela dinâmica.  
  
    4.  Escolha a coluna de origem que fornece os valores de membros de atributo traduzidos. Somente colunas já existentes na tabela ou consulta associada à dimensão estão disponíveis. Se a coluna não existir, você precisa modificar a exibição da fonte de dados, dimensão e cubo para selecionar a coluna.  
  
    5.  Escolha a ordem de ordenação e de classificação, se aplicável.  
  
4.  Compilar e implantar o projeto.  
  
5.  Conecte-se ao banco de dados usando um aplicativo cliente, como o Excel, modificando a cadeia de conexão para usar o identificador de localidade. Consulte [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) para obter detalhes.  
  
### <a name="add-a-translation-of-the-database-name"></a>Adicionar uma tradução do nome do banco de dados  
 No nível do banco de dados, você pode adicionar traduções para o nome do banco de dados e descrição. O nome do banco de dados traduzido pode estar visível nas conexões de cliente que especificam o LCID do idioma, mas que depende da ferramenta. Por exemplo, exibir o banco de dados no Management Studio não mostrará o nome traduzido, mesmo que você especifique o identificador de localidade na conexão. A API usada pelo Management Studio para se conectar ao Analysis Services não lê a propriedade `Language`.  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no nome do projeto | **Editar banco de dados** para abrir o designer de banco de dados.  
  
2.  Em Traduções, especifique o idioma de destino (resolve para um LCID), legenda traduzida e descrição traduzida. A lista de idiomas é consistente em todo o Analysis Services, se você estiver definindo o idioma do servidor no Management Studio ou adicionando uma substituição de tradução em um único atributo.  
  
3.  Na página Propriedades do banco de dados, defina `Language` com o mesmo LCID especificado para a tradução. Opcionalmente, defina `Collation` também se o padrão não fizer mais sentido.  
  
4.  Compilar e implantar o banco de dados.  
  
## <a name="resolving-translations"></a>Resolvendo traduções  
 Se um aplicativo cliente solicita um identificador de localidade, a instância [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tenta resolver dados e metadados para objetos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para o LCID correspondente mais próximo. Se o aplicativo cliente não especificar um idioma padrão, especificar o identificador de localidade neutro (0) ou identificador de idioma padrão (1024), o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usará o idioma padrão para a instância para retornar dados e metadados para objetos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Cenários de globalização para Analysis Services multidimensional](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Linguagens e agrupamentos &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)   
 [Definir ou alterar o agrupamento de colunas](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Dicas de globalização e práticas recomendadas &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)  
  
  
