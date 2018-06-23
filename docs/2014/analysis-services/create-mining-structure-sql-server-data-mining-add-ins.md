---
title: Criar estrutura de mineração (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining structures, creating
ms.assetid: b8b1eedc-4d6d-4429-a578-e629ec573934
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 415540535e6456dcead8ca749d8fe0f2fbae5150
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116483"
---
# <a name="create-mining-structure-sql-server-data-mining-add-ins"></a>Criar estrutura de mineração (Suplementos de Mineração de Dados do SQL Server)
  ![Criar botão de estrutura de mineração, faixa de opções mineração de dados](media/dmc-createstruct.gif "botão Criar estrutura de mineração, faixa de opções mineração de dados")  
  
 Use o **avançado** opção o **modelagem de dados** grupo quando você deseja criar um conjunto de dados usado para análise sem necessariamente criar um modelo. Isso é útil quando você deseja testar algoritmos diferentes.  
  
 Depois de ter criado a estrutura de mineração, use o [Adicionar modelo à estrutura](add-model-to-structure-data-mining-add-ins-for-excel.md) Assistente para criar um modelo com base nessa estrutura. Você também pode criar novos modelos usando o **Editor mineração de dados avançado consulta**.  
  
 Você também pode usar essa opção quando pretende criar modelos usando um dos algoritmos avançados, que têm suporte do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] mas não estão disponíveis por meio de um assistente, como a regressão linear ou o clustering de sequências, ou se você estiver usando um algoritmo personalizado.  
  
> [!NOTE]  
>  Quando você cria a estrutura de mineração, também pode estabelecer um conjunto de dados de teste selecionado aleatoriamente a ser usado para validar todos os seus modelos. Isso é útil porque você pode facilmente comparar a precisão do modelo em um conjunto de dados comum. Selecione a opção **dividir os dados em conjuntos de teste e treinamento** e especifique uma porcentagem apropriada de dados para reservar para teste, normalmente em torno 30 por cento.  
  
## <a name="use-the-wizard-to-create-a-mining-structure"></a>Usar o assistente para criar uma estrutura de mineração  
  
1.  No **mineração de dados** de faixa de opções, clique em **avançado**e selecione **criar estrutura**.  
  
2.  No **selecionar dados de origem** caixa de diálogo, especifique o intervalo do Excel, a tabela de dados do Excel ou a fonte de dados externa que contém os dados que você deseja usar para análise.  
  
     Clique em **Avançar**.  
  
3.  No **selecionar colunas** caixa de diálogo caixa, examine a lista de colunas disponíveis na fonte de dados selecionada.  
  
4.  Clique na seta à direita do nome da coluna para alterar o **uso** da coluna, escolhendo a partir desses valores:  
  
    -   **Key**. Cada modelo exige pelo menos uma chave.  
  
    -   **Hora da chave**. Essa opção só está disponível para modelos de previsão, onde ela é necessária.  
  
    -   **Incluir**. Indica que a coluna deve ser disponibilizada na estrutura de mineração, mas ela não é uma coluna de chave.  
  
    -   **Não use**. Indica que a coluna não deve ser incluída na estrutura de mineração.  
  
     Lembre-se de que sempre é possível ignorar colunas quando você cria o modelo, mas, para adicionar colunas posteriormente, você precisa reprocessar a estrutura e o modelo.  
  
5.  Clique no botão Procurar **(...)**  botão para definir o tipo de conteúdo, tipo de dados e sinalizadores de modelagem.  
  
    > [!NOTE]  
    >  Se a coluna contiver dados numéricos, procure sempre abrir esta caixa de diálogo para garantir que o tipo de dados correto seja escolhido. Em alguns casos, mesmo se os dados de entrada forem um número, você desejará tratá-los como uma variável categórica, ou um valor discreto, e não como um número contínuo.  
    >   
    >  Por exemplo, uma coluna de CEP pode ser listada por padrão como um tipo de dados longo contínuo, mas, para obter resultados melhores, especifique que ela será tratada como um valor de texto discreto.  
    >   
    >  Para obter mais informações, consulte a seção sobre tipos de conteúdo em [escolhendo dados para mineração de dados](choosing-data-for-data-mining.md).  
  
     Clique em **OK** para fechar a caixa de diálogo.  
  
6.  Clique em **Avançar**.  
  
     Dependendo do tipo de dados utilizado, você poderá concluir o assistente após essa etapa. Nesse caso, ir para o **concluir** página para nomear sua estrutura de mineração.  
  
     Para outros modelos, você tem a opção adicional de criar um conjunto de dados de teste.  
  
7.  No **dividir os dados em conjuntos de dados de treinamento e teste** caixa de diálogo, especifique como você deseja particionar os dados. Por padrão, 30% dos dados são usados para teste.  
  
     Se desejar, digite o número máximo de linhas a serem usadas para teste.  
  
     Clique em **Avançar**.  
  
8.  No **concluir** caixa de diálogo, digite um nome e uma descrição para a nova estrutura de mineração.  
  
9. Clique em **Concluir**.  
  
### <a name="related-options"></a>Opções relacionadas  
  
|Opção|Comentários|  
|------------|--------------|  
|**Selecione a fonte de dados** caixa de diálogo|Quando você seleciona uma tabela do Excel, deve indicar se os dados já têm cabeçalhos. Se você ignorar isso, a primeira linha de dados será usada como o nome da coluna.<br /><br /> Se você usar a opção **fonte de dados externa**, você pode usar qualquer tipo de dados que podem ser definidos em um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fonte de dados. Entretanto, a caixa de diálogo no suplemento para criar novas fontes de dados não inclui a gama completa de fontes de dados com suporte do Analysis Services; portanto, é recomendável criar fontes de dados no servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] antecipadamente e conectá-las com os suplementos.|  
|**Editor de consulta de fonte de dados** caixa de diálogo|Após se conectar à fonte de dados especificada, você pode adicionar colunas, ou criar uma consulta personalizada para gerar colunas personalizadas.|  
|**Dividir os dados em conjuntos de dados de treinamento e teste**|Um valor recomendado para treinamento vs. conjuntos de teste é 70% para treinamento e 30% para teste; No entanto, se você tiver muitos dados, você pode especificar um número máximo de linhas para teste.|  
|Caixa de diálogo Concluir|As opções para detalhamento estão disponíveis em alguns tipos de modelo e são muito úteis se você incluiu colunas de detalhes na estrutura de mineração. Por exemplo, se você criar um modelo de clustering, poderá incluir detalhes como o nome ou o endereço de email para o detalhamento, mas não a análise, para facilitar o contato com clientes em um cluster específico.|  
  
###  <a name="Bkmk_strctcolumn"></a> Definindo o uso de coluna na criar Assistente de estrutura de mineração  
 Ao criar uma nova estrutura de mineração, você pode especificar quais colunas da fonte de dados deverão ser incluídas na estrutura de mineração e como essas colunas deverão ser usadas. Lembre-se de que uma estrutura de mineração pode oferecer suporte a vários modelos de mineração.  
  
|Valores|Description|  
|------------|-----------------|  
|**Incluir**|Especifica que a coluna contém dados que podem ser usados para análise ou previsão.|  
|**Chave**|Especifica que a coluna contém uma ID de transação, uma ID de série ou outra chave necessária para processamento.<br /><br /> Todos os algoritmos requerem uma coluna Key. Porém, alguns algoritmos permitem apenas uma única chave, enquanto outros permitem várias chaves.<br /><br /> Se a coluna contiver uma chave, mas não é necessária para o processamento, selecione **não usar**.|  
|**Chave de tempo**|Especifica que a coluna contém uma data ou outro valor numérico que pode ser usado para identificar os itens de uma série temporal de maneira exclusiva.|  
|**Não Use**|Especifica que a coluna deve ser ignorada. Os dados na coluna não serão processados.|  
  
 Para processar corretamente um modelo, o algoritmo precisará saber quais colunas são a coluna de chave que identifica exclusivamente cada uma das linhas; qual coluna é a coluna de destino para a criação de previsões, caso se esteja criando um modelo previsível, e quais colunas usar como colunas de entrada para criar relações que preveem a coluna de destino.  
  
-   Colunas que são especificadas como **não use** não estarão presentes na estrutura de mineração.  
  
     Se você adicionar colunas desnecessárias ou com valores inválidos, isso poderá prejudicar os resultados da análise. Portanto, assegure-se de incluir apenas as colunas que sejam relevantes. Contudo, lembre-se de que as colunas não utilizadas na estrutura de mineração não estarão disponíveis para consultas.  
  
-   Colunas que são especificadas como o **incluir** tipo será incluído na estrutura de mineração e posteriormente pode ser usado para análise ou previsão nos modelos de mineração.  
  
     Caso não tenha certeza se precisará usar a coluna, você sempre poderá incluí-la na estrutura de mineração e depois criar um modelo de mineração que não utilize a coluna. Por exemplo, é possível incluir uma coluna de número de telefone nos dados para referência posterior, mas criar um modelo de clustering que ignore números de telefone. Após a criação dos clusters, você pode criar uma consulta que retorne os números de telefone das pessoas que pertençam a um cluster específico.  
  
-   Todos os algoritmos requerem uma **chave** coluna. Os valores na coluna Key devem ser exclusivos. Um **Key Time** coluna é necessária apenas para previsão ou de série temporal modelos. para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
### <a name="requirements"></a>Requisitos  
 Para criar uma estrutura de mineração de dados, você deve ter uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Uma conexão será necessária mesmo que você esteja trabalhando com estruturas temporárias. Para obter mais informações sobre como criar ou alterar uma conexão, consulte [conectar-se à fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)  
  
  