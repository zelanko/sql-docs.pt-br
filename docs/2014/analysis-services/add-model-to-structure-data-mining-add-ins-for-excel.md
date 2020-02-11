---
title: Adicionar modelo à estrutura (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce68071f27897e181063299e561dfaa7d9f8aab7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062882"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>Adicionar modelo à estrutura (Suplementos de Mineração de Dados para Excel)
  ![Botão Adicionar Modelo à Estrutura](media/dmc-addmodel.gif "Botão Adicionar Modelo à Estrutura")  
  
 Quando você clica em **Adicionar modelo à estrutura**, um assistente é iniciado para ajudá-lo a criar um novo modelo de mineração para usar com uma estrutura de mineração existente. Essa opção é útil porque permite comparar modelos baseados nos mesmos dados, ou criar modelos personalizados.  
  
 Se a instância do Analysis Services ainda não contiver os dados necessários, use o assistente para [criar estrutura de mineração &#40;SQL Server suplementos de mineração de dados&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) para configurar uma estrutura de mineração. Ou você poderá iniciar um dos assistentes de modelagem e adicionar um novo modelo à estrutura criada pelo assistente.  
  
 Para criar modelos avançados usando algoritmos sem suporte nos assistentes, crie uma estrutura de mineração e, em seguida, adicione um modelo usando o **Editor de consulta avançada de mineração de dados**.  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>Adicionar um modelo novo a uma estrutura existente  
  
1.  Na faixa de opções **mineração de dados** , clique na seta em **avançado**e, em seguida, selecione **Adicionar modelo à estrutura**.  
  
2.  Na caixa de diálogo **selecionar estrutura** , escolha a estrutura que contém os dados que você deseja usar e clique em **Avançar**.  
  
     **Dica**: se você não tiver certeza de qual estrutura de mineração contém os dados necessários, use o assistente de **modelo de documento** para exibir as colunas e as estatísticas básicas sobre os dados.  
  
     Se você não encontrar uma estrutura de mineração, verifique a conexão que você está usando no momento. Talvez você precise abrir uma conexão com um servidor diferente.  
  
3.  Na caixa de diálogo **selecionar algoritmo de mineração** , escolha um algoritmo de mineração para usar no novo modelo de mineração.  
  
     Observe que a caixa de diálogo fornece muito mais opções do que você verá nos assistentes. Você pode criar um modelo usando qualquer algoritmo com suporte do servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], desde que seus dados sejam compatíveis.  
  
4.  Recomendamos que você também clique no botão **parâmetros** para abrir a caixa de diálogo **parâmetros de algoritmo** e personalizar parâmetros no algoritmo. Essa opção é a maneira mais fácil de criar modelos de mineração personalizados.  
  
5.  Clique em **Próximo**.  
  
6.  Na caixa de diálogo **selecionar colunas** , examine a lista de colunas e, se necessário, altere o uso das colunas para um destes valores:  
  
    -   **Entrada**. Indica que a coluna contém variáveis que podem afetar o resultado e devem ser usadas como entradas para o modelo.  
  
    -   **Entrada e previsão**. Indica que os dados devem ser usados como uma entrada e que você também deseja prever esses valores.  
  
    -   **Somente previsão**. Indica que os dados não devem ser usados como uma entrada para o modelo.  
  
    -   **Chave**. Cada modelo requer pelo menos uma chave. Dependendo do tipo de modelo, você também pode ter a opção de chaves especiais adicionais, como **SequenceKey** ou **TimeKey**.  
  
    -   Não **use**. Indica que os dados não devem ser usados no modelo, mesmo se presentes na estrutura.  
  
7.  Clique no botão procurar **(...)** para abrir a caixa de diálogo **definir sinalizadores de modelo de coluna** .  
  
     Reserve um minuto para verificar se o uso de cada coluna de dados é apropriado para o modelo. Essa é uma etapa importante para evitar erros ao tentar processar o modelo.  
  
     Por exemplo, se você reutilizar uma estrutura que foi criada para um modelo de árvores de decisão e aplicar o algoritmo Naïve Bayes a ela, as colunas com o tipo de dados `Numeric` e o tipo de conteúdo `Continuous` precisarão ser compartimentadas ou alteradas para as variáveis discretas.  
  
     Se as colunas na estrutura não forem aplicáveis ao novo algoritmo, você poderá ignorá-las selecionando não **usar**.  
  
8.  Na caixa de diálogo **definir sinalizadores de modelo de coluna** , revise ou defina os sinalizadores de modelagem, se houver.  
  
     Os sinalizadores de modelagem permitem controlar a maneira como nulos são tratados, entre outras coisas. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](data-mining/modeling-flags-data-mining.md).  
  
     Clique em **OK** quando terminar para fechar a caixa de diálogo.  
  
9. Na caixa de diálogo **concluir** , digite um nome e uma descrição para o novo modelo de mineração.  
  
     Dependendo do tipo de modelo criado, você também poderá ter as seguintes opções:  
  
    -   Procurar o modelo de mineração completo após sua criação.  
  
    -   Usar o detalhamento do modelo para os dados de origem.  
  
         Para obter mais informações, consulte [detalhamento em modelos de mineração](data-mining/drillthrough-on-mining-models.md).  
  
10. Clique em **concluir** para salvar as alterações. Quando você faz isso, o novo modelo é implantado no servidor e processado.  
  
### <a name="related-options"></a>Opções relacionadas  
  
|Opção|Comentários|  
|------------|--------------|  
|Caixa **de diálogo Selecionar estrutura ou modelo**|Escolha uma estrutura de mineração existente para usar como a base para criar um novo modelo.  A estrutura que você escolhe deve estar localizada na conexão atual. Caso contrário, altere as conexões usando a ferramenta [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md) .|  
|Caixa de diálogo **selecionar algoritmo de mineração**|A lista de algoritmos de mineração de dados varia de acordo com o servidor ao qual você está conectado. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece algoritmos diferentes nas edições Standard e Enterprise. O administrador também pode ter adicionado algoritmos personalizados.<br /><br /> Se você não puder ver algoritmos, verifique se você está conectado a uma instância [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]do.|  
|**Parâmetros de algoritmo** Caixa de diálogo|Nessas configurações, você pode personalizar cada algoritmo usando parâmetros específicos ao método analítico. Você também pode definir uma semente para garantir que os resultados do modelo possam ser reproduzidos nas passagens de treinamento.<br /><br /> Para obter mais informações, consulte [parâmetros de algoritmo &#40;SQL Server suplementos de mineração de dados&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md).|  
|**Definir sinalizadores de modelo de coluna** Caixa de diálogo|Os sinalizadores de modelagem podem melhorar seu modelo especificando como os dados ausentes devem ser tratados. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](data-mining/modeling-flags-data-mining.md).|  
  
###  <a name="Bkmk_mdlcolumn"></a>Definindo o uso da coluna  
 Ao adicionar um novo modelo a uma estrutura de mineração existente, você deverá especificar como o modelo usará cada coluna de dados na estrutura de mineração. Você provavelmente observará que as opções neste assistente são muito mais detalhadas do que as opções na estrutura de mineração. Por quê?  
  
 Isso ocorre porque, quando você cria um modelo e uma estrutura juntos usando um assistente, muitas das opções que controlam a forma como os dados são usados pelo algoritmo são definidas automaticamente. No entanto, ao adicionar um novo modelo a um existente, você precisa ver essas opções manualmente e especificar se os dados devem ser usados para análise, se o tipo de dados está correto e assim por diante.  
  
 Talvez você receba mensagens de erro ao aplicar novos algoritmos a dados existentes, mas essas mensagens geralmente fornecem informações detalhadas sobre as correções que você precisa fazer para permitir que o modelo seja processado. Problemas típicos incluem o seguinte:  
  
-   O modelo espera um tipo de dados diferente daquele que a estrutura contém.  
  
     Alguns algoritmos só funcionam com números; outros só funcionam com texto. Se os dados forem do tipo incorreto para o novo modelo, talvez você precise modificar a estrutura para permitir que o modelo seja processado.  
  
-   A estrutura de mineração não contém atributos previsíveis.  
  
     Modelos de clustering podem ser criados sem valor previsível, mas outros modelos normalmente exigem que você especifique uma única coluna para previsão.  
  
-   A composição dos dados é incompatível com o algoritmo que você escolheu.  
  
     Alguns tipos de análise exigem que os dados sejam estruturados com cuidado, de acordo com regras exclusivas. Os exemplos são modelos de previsão e modelos de associação. Você pode facilmente adicionar novos modelos do mesmo tipo, talvez com personalizações, mas os dados talvez não funcionem com outros algoritmos.  
  
### <a name="requirements"></a>Requisitos  
 Para criar modelos de mineração de dados, você deve ter uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter mais informações sobre como criar ou alterar uma conexão, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Caso você não consiga visualizar a estrutura de mineração de dados desejada, talvez ela tenha sido salva em outra instância ou em outro banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter informações sobre como alterar para uma conexão de Data Mining diferente, consulte [conectar-se a um servidor de mineração de dados](connect-to-a-data-mining-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
