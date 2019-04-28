---
title: Criar uma nova estrutura de mineração OLAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], OLAP
- mining structures [Analysis Services], creating
- OLAP [Analysis Services], mining models
ms.assetid: 368f4273-a016-4748-bcb6-505a3e745af3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 603b1d22370a32808460aa3e725e5f26e0f62dc0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62718203"
---
# <a name="create-a-new-olap-mining-structure"></a>Criar uma nova estrutura de mineração OLAP
  Você pode usar o Assistente de Mineração de Dados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para criar uma estrutura de mineração que usa dados de um modelo multidimensional. Modelos de mineração baseados em cubos OLAP podem usar a coluna e os valores de tabelas de fatos, dimensões e grupos de medidas como atributos para análise.  
  
### <a name="to-create-a-new-olap-mining-structure"></a>Para criar uma nova estrutura de mineração OLAP  
  
1.  No Gerenciador de Soluções do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse na pasta **Estruturas de Mineração** de um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Nova Estrutura de Mineração** para abrir o Assistente de Mineração de Dados.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **Selecionar o Método de Definição** , selecione **De cubo existente**e clique em **Avançar**.  
  
     Se você receber um erro com a mensagem Não é possível recuperar uma lista de algoritmos de mineração de dados aceitos, abra a caixa de diálogo **Propriedades do Projeto** e verifique se especificou o nome de uma instância do Analysis Services que dá suporte a modelos multidimensionais. Não é possível criar modelos de mineração em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que oferece suporte à modelagem de tabela.  
  
4.  Na página **Criar a Estrutura de Mineração de Dados** , decida se você criará somente uma estrutura de mineração ou uma estrutura de mineração, além de um modelo de mineração relacionado. Em geral, é mais fácil criar um modelo de mineração ao mesmo tempo para que você seja solicitado a incluir as colunas necessárias.  
  
     Se você criar um modelo de mineração, selecione o algoritmo de mineração de dados que você quer usar e clique em **Avançar**. Para obter mais informações sobre como escolher um algoritmo, consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de dados &#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  Na página **Selecionar a Dimensão do Cubo de Origem**, em **Selecionar uma Dimensão do Cubo de Origem**, localize a dimensão que contém a maioria de seus dados de caso.  
  
     Por exemplo, se estiver tentando identificar agrupamentos de clientes, poderá escolher a dimensão Cliente; se estiver tentando analisar compras em transações, poderá escolher a dimensão Detalhes do Pedido de Vendas pela Internet. Você não está restrito a usar somente os dados desta dimensão, mas ela deve conter atributos importantes a serem usados na análise.  
  
     Clique em **Avançar**.  
  
6.  Na página **Selecionar a Chave do Caso** , em **Atributos**, selecione o atributo que será a chave da estrutura de mineração e clique em **Avançar**.  
  
     O atributo que você costuma usar como chave na estrutura de mineração também é uma chave da dimensão e será pré-selecionado.  
  
7.  Na página **Selecionar Colunas de Nível de Caso** , em **Atributos e Medidas Relacionados**, selecione os atributos e as medidas que contêm valores a serem adicionados à estrutura de mineração como dados de caso. Clique em **Avançar**.  
  
8.  Na página **Especificar Uso de Colunas do Modelo de Mineração** , em **Estrutura do modelo de mineração**, primeiro defina a coluna previsível e depois escolha colunas para usar como entradas.  
  
    -   Marque a caixa de seleção na coluna à extrema esquerda para incluir os dados na estrutura de mineração. Você pode incluir colunas na estrutura que usará para referência, mas não usá-las para análise.  
  
    -   Marque a caixa de seleção na coluna **Entrada** para usar o atributo como uma variável na análise.  
  
    -   Marque a caixa de seleção na coluna **Prever** somente para atributos previsíveis.  
  
     Note que as colunas designadas como chaves não podem ser usadas para entrada nem previsão.  
  
     Clique em **Avançar**.  
  
9. Na página **Especificar Uso de Colunas do Modelo de Mineração** , você também pode adicionar e remover tabelas aninhadas da estrutura de mineração, usando **Adicionar Tabelas Aninhadas** e **Tabelas Aninhadas**.  
  
     Em um modelo de mineração de OLAP, uma tabela aninhada é outro conjunto de dados dentro do cubo que tem uma relação um-para-muitos com a dimensão que representa os atributos de caso. Portanto, quando a caixa de diálogo for aberta, ela selecionará previamente grupos de medidas que já estão relacionados à dimensão selecionada como a tabela de casos. Neste ponto, você escolheria uma dimensão diferente que contém informações adicionais úteis para análise.  
  
     Por exemplo, se estiver analisando clientes, você usará a dimensão [Cliente] como a tabela de casos. Para a tabela aninhada, você pode adicionar o motivo citado pelos clientes ao fazer uma compra, que está incluído na dimensão [Motivo de Vendas].  
  
     Se você adicionar dados aninhados, especifique duas colunas adicionais:  
  
    -   A chave da tabela aninhada: Isso deve ser pré-selecionada na página de **selecionar chave de tabela aninhada**.  
  
    -   Os atributos ou atributos usados para análise: A página **selecionar colunas de tabela aninhada**, fornece uma lista de medidas e atributos na seleção da tabela aninhada.  
  
        -   Para cada atributo incluído no modelo, marque a caixa na coluna esquerda.  
  
        -   Se quiser usar apenas o atributo para análise, marque a opção **Entrada**.  
  
        -   Se quiser incluir a coluna como um dos atributos previsíveis do modelo, selecione **Prever**.  
  
        -   Qualquer item incluído na estrutura, mas não especificado como uma entrada ou atributo previsível, é adicionado à estrutura com o sinalizador `Ignore`; isso significa que os dados são processados quando você cria o modelo, mas não são usado na análise, e estão disponíveis apenas para detalhamento. Isso pode ser útil se você deseja incluir detalhes como nomes de clientes, mas não quiser usá-los na análise.  
  
     Clique em **Concluir** para fechar a parte do assistente que trabalha com tabelas aninhadas. Você pode repetir o processo para adicionar varias colunas aninhadas.  
  
10. Na página **Especificar Conteúdo e Tipos de Dados das Colunas** , em **Estrutura de modelo de mineração**, defina o tipo de conteúdo e o tipo de dados para cada coluna.  
  
    > [!NOTE]  
    >  Os modelos de mineração OLAP não permitem o uso do recurso **Detectar** para detectar automaticamente se uma coluna contém dados contínuos ou distintos.  
  
     Clique em **Avançar**.  
  
11. Na página **Dividir Cubo de Origem** , é possível filtrar os dados usados para criar a estrutura de mineração.  
  
     A divisão do cubo lhe permite restringir os dados que são usados para criar o modelo. Por exemplo, você pode criar modelos separados para cada região dividindo a hierarquia Geografia e  
  
    -   **Dimensão**: Escolha uma dimensão relacionada na lista suspensa.  
  
    -   **Hierarquia**:  Selecione o nível da hierarquia de dimensão na qual você deseja aplicar o filtro. Por exemplo, se estiver dividindo pela dimensão [Geografia], você escolherá um nível de hierarquia como [Nome do País da Região].  
  
    -   **Operador**: Escolha um operador na lista.  
  
    -   **Expressão de filtro**: Digite um valor ou expressão para servir como a condição de filtro ou use a lista suspensa para selecionar um valor na lista de membros no nível da hierarquia especificado.  
  
         Por exemplo, se você selecionar [Geografia] como a dimensão e [Nome do País da Região] como o nível de hierarquia, a lista suspensa conterá todos os países válidos que você pode usar como uma condição de filtro. Você pode fazer várias seleções. Como resultado, os dados na estrutura de mineração serão limitados a dados de cubo destas áreas geográficas.  
  
    -   **Parâmetros**: Ignore esta caixa de seleção. Esta caixa de diálogo oferece suporte a vários cenários de filtragem de cubo e esta opção não é relevante para criar uma estrutura de mineração.  
  
     Clique em **Avançar**.  
  
12. Na página **Dividir os dados em conjuntos de treinamento e teste** , especifique um percentual dos dados da estrutura de mineração a ser reservado para teste ou especifique o número máximo de casos de teste. Clique em **Avançar**.  
  
     Se você especificar ambos os valores, os limites serão combinados para usar o que for o mais baixo.  
  
13. Na página **Concluindo o Assistente** , forneça um nome para a nova estrutura de mineração OLAP e para o modelo de mineração inicial.  
  
14. Clique em **Concluir**.  
  
15. Na página **Concluindo o Assistente** , você também tem a opção de criar uma dimensão do modelo de mineração e/ou um cubo usando a dimensão do modelo de mineração. Estas opções têm suporte apenas para modelos criados usando os seguintes algoritmos:  
  
    -   Algoritmo Microsoft Clustering  
  
    -   Algoritmo Árvores de Decisão da Microsoft  
  
    -   Algoritmo de Regras de Associação da Microsoft  
  
     **Criar dimensão do modelo de mineração**: Marque essa caixa de seleção e forneça um nome de tipo para a dimensão do modelo de mineração. Quando você usar esta opção, uma nova dimensão será criada no cubo original que foi usado para criar a estrutura de mineração. Você pode usar esta dimensão para detalhar e conduzir análises adicionais. Como a dimensão está localizada no cubo, a dimensão é mapeada automaticamente para a dimensão de dados de caso.  
  
     **Criar cubo usando a dimensão do modelo de mineração**: Marque essa caixa de seleção e forneça um nome para o novo cubo. Quando você usa esta opção, um novo cubo é criado, contendo as dimensões existentes, que foram usadas para criar a estrutura, e a nova dimensão de mineração de dados, contendo os resultados do modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
  
