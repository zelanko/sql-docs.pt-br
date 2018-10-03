---
title: Adicionar modelo à estrutura (Data Mining Add-ins para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cbbbbcd154642ef3437b0860d8346d76f84bd97
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104786"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>Adicionar modelo à estrutura (Suplementos de Mineração de Dados para Excel)
  ![Adicionar modelo de botão de estrutura](media/dmc-addmodel.gif "Add Model ao botão de estrutura")  
  
 Quando você clica em **Adicionar modelo à estrutura**, é iniciado um assistente que ajuda você a cria um novo modelo de mineração para usar com uma estrutura de mineração existente. Essa opção é útil porque permite comparar modelos baseados nos mesmos dados, ou criar modelos personalizados.  
  
 Se a instância do Analysis Services ainda não contiver dados que você precisa, use o [criar estrutura de mineração &#40;SQL Server Data Mining Add-ins&#41; ](create-mining-structure-sql-server-data-mining-add-ins.md) Assistente para configurar uma estrutura de mineração. Ou você poderá iniciar um dos assistentes de modelagem e adicionar um novo modelo à estrutura criada pelo assistente.  
  
 Para criar modelos avançados usando algoritmos que não tem suportados dos assistentes, crie uma estrutura de mineração e, em seguida, adicione um modelo usando o **Editor de consulta avançada de mineração de dados**.  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>Adicionar um modelo novo a uma estrutura existente  
  
1.  Sobre o **Data Mining** faixa de opções, clique na seta sob **avançado**e, em seguida, selecione **Adicionar modelo à estrutura**.  
  
2.  No **selecionar estrutura** diálogo caixa, escolha a estrutura que contém os dados que você deseja usar e, em seguida, clique em **próxima**.  
  
     **Dica**: se você não tiver certeza de qual estrutura de mineração contém os dados necessários, use o **modelo de documento** Assistente para exibir as colunas e estatísticas básicas sobre os dados.  
  
     Se você não conseguir encontrar uma estrutura de mineração, verifique a conexão que está usando no momento. Talvez você precise abrir uma conexão com um servidor diferente.  
  
3.  No **Selecionar algoritmo de mineração** caixa de diálogo, escolha um algoritmo de mineração usar no novo modelo de mineração.  
  
     Observe que a caixa de diálogo fornece muito mais opções do que aparecem nos assistentes. Você pode criar um modelo usando qualquer algoritmo com suporte do servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], desde que seus dados sejam compatíveis.  
  
4.  É recomendável que você clique também o **parâmetros** para abrir o **parâmetros de algoritmo** caixa de diálogo caixa e personalizar os parâmetros no algoritmo. Essa opção é a maneira mais fácil de criar modelos de mineração personalizados.  
  
5.  Clique em **Avançar**.  
  
6.  No **selecionar colunas** caixa de diálogo, examine a lista de colunas e, se necessário, altere o uso das colunas para um destes valores:  
  
    -   **Entrada**. Indica que a coluna contém variáveis que podem afetar o resultado e devem ser usadas como entradas para o modelo.  
  
    -   **Inserir e prever**. Indica que os dados devem ser usados como uma entrada e que você também deseja prever esses valores.  
  
    -   **Prever apenas**. Indica que os dados não devem ser usados como uma entrada para o modelo.  
  
    -   **Key**. Cada modelo exige pelo menos uma chave. Dependendo do tipo de modelo, você pode também ter a opção de chaves especiais adicionais, como o **SequenceKey** ou **TimeKey**.  
  
    -   **Não use**. Indica que os dados não devem ser usados no modelo, mesmo se presentes na estrutura.  
  
7.  Clique no botão Procurar **(...)**  para abrir o **definir sinalizadores de modelo da coluna** caixa de diálogo.  
  
     Reserve um minuto para verificar se o uso de cada coluna de dados é apropriado para o modelo. Essa é uma etapa importante para evitar erros ao tentar processar o modelo.  
  
     Por exemplo, se você reutilizar uma estrutura que foi criada para um modelo de árvores de decisão e aplicar o algoritmo Naïve Bayes a ela, as colunas com o tipo de dados `Numeric` e o tipo de conteúdo `Continuous` precisarão ser compartimentadas ou alteradas para as variáveis discretas.  
  
     Se as colunas na estrutura não são aplicáveis ao novo algoritmo, você pode ignorá-las selecionando **não use**.  
  
8.  No **definir sinalizadores de modelo da coluna** caixa de diálogo, revise ou conjunto de sinalizadores de modelagem, se houver.  
  
     Os sinalizadores de modelagem permitem controlar a maneira como nulos são tratados, entre outras coisas. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](data-mining/modeling-flags-data-mining.md).  
  
     Clique em **Okey** ao concluir para fechar a caixa de diálogo.  
  
9. No **concluir** caixa de diálogo, digite um nome e uma descrição para o novo modelo de mineração.  
  
     Dependendo do tipo de modelo criado, você também poderá ter as seguintes opções:  
  
    -   Procurar o modelo de mineração completo após sua criação.  
  
    -   Usar o detalhamento do modelo para os dados de origem.  
  
         Para obter mais informações, consulte [detalhamento em modelos de mineração](data-mining/drillthrough-on-mining-models.md).  
  
10. Clique em **concluir** para salvar suas alterações. Quando você faz isso, o novo modelo é implantado no servidor e processado.  
  
### <a name="related-options"></a>Opções relacionadas  
  
|Opção|Comentários|  
|------------|--------------|  
|**Selecionar estrutura ou modelo** caixa de diálogo|Escolha uma estrutura de mineração existente para usar como a base para criar um novo modelo.  A estrutura que você escolhe deve estar localizada na conexão atual. Se não estiver, altere as conexões usando o [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41; ](connect-to-source-data-data-mining-client-for-excel.md) ferramenta.|  
|**Selecione o algoritmo de mineração de** caixa de diálogo|A lista de algoritmos de mineração de dados varia de acordo com o servidor ao qual você está conectado. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece algoritmos diferentes nas edições Standard e Enterprise. O administrador também pode ter adicionado algoritmos personalizados.<br /><br /> Se você não conseguir ver algoritmos, verifique se está conectado a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|**Parâmetros do algoritmo** caixa de diálogo|Nessas configurações, você pode personalizar cada algoritmo usando parâmetros específicos ao método analítico. Você também pode definir uma semente para garantir que os resultados do modelo possam ser reproduzidos nas passagens de treinamento.<br /><br /> Para obter mais informações, consulte [parâmetros de algoritmo &#40;SQL Server Data Mining Add-ins&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md).|  
|**Definir sinalizadores de modelo da coluna** caixa de diálogo|Os sinalizadores de modelagem podem melhorar seu modelo especificando como os dados ausentes devem ser tratados. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](data-mining/modeling-flags-data-mining.md).|  
  
###  <a name="Bkmk_mdlcolumn"></a> Definindo o uso de coluna  
 Ao adicionar um novo modelo a uma estrutura de mineração existente, você deverá especificar como o modelo usará cada coluna de dados na estrutura de mineração. Provavelmente você notará que as opções nesse assistente são bem mais detalhadas do que as opções na estrutura de mineração. Por quê?  
  
 Isso ocorre porque, quando você cria um modelo e uma estrutura juntos usando um assistente, muitas das opções que controlam a forma como os dados são usados pelo algoritmo são definidas automaticamente. No entanto, ao adicionar um novo modelo a um existente, você precisa ver essas opções manualmente e especificar se os dados devem ser usados para análise, se o tipo de dados está correto e assim por diante.  
  
 Talvez você receba mensagens de erro ao aplicar novos algoritmos a dados existentes, mas essas mensagens geralmente fornecem informações detalhadas sobre as correções que você precisa fazer para permitir que o modelo seja processado. Problemas típicos incluem o seguinte:  
  
-   O modelo espera um tipo de dados diferente daquele que a estrutura contém.  
  
     Alguns algoritmos só funcionam com números; outros só funcionam com texto. Se os dados forem do tipo incorreto para o novo modelo, talvez você precise modificar a estrutura para permitir que o modelo seja processado.  
  
-   A estrutura de mineração não contém atributos previsíveis.  
  
     Modelos de clustering podem ser criados sem valor previsível, mas outros modelos normalmente exigem que você especifique uma única coluna para previsão.  
  
-   A composição dos dados é incompatível com o algoritmo escolhido.  
  
     Alguns tipos de análise exigem que os dados sejam estruturados com cuidado, de acordo com regras exclusivas. Os exemplos são modelos de previsão e modelos de associação. Você pode facilmente adicionar novos modelos do mesmo tipo, talvez com personalizações, mas os dados talvez não funcionem com outros algoritmos.  
  
### <a name="requirements"></a>Requisitos  
 Para criar modelos de mineração de dados, você deve ter uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter mais informações sobre como criar ou alterar uma conexão, consulte [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Caso você não consiga visualizar a estrutura de mineração de dados desejada, talvez ela tenha sido salva em outra instância ou em outro banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter informações sobre como mudar para uma conexão de mineração de dados diferentes, consulte [conectar-se a um servidor de mineração de dados](connect-to-a-data-mining-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)   
