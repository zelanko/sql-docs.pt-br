---
title: Exemplo de dados (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- holdout
- testing cases
- training cases
- partitioning data [data mining]
- mining models, testing
ms.assetid: 35907ae6-887f-4cb3-a750-cff3d7683d90
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a69b2286abbc1ba4289fd482b1bbf5a2dfb3e7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070035"
---
# <a name="sample-data-sql-server-data-mining-add-ins"></a>Dados de Amostra (Suplementos de Mineração de Dados do SQL Server)
  ![Assistente de partição de dados na faixa de opções mineração de dados](media/dmc-partition.gif "Assistente particionar os dados na faixa de opções mineração de dados")  
  
 O **dados de exemplo** assistente facilita a divisão da fonte de dados em dois conjuntos, um para criar (treinar) o modelo e outra para testar o modelo. Esse assistente também fornece uma opção para gerar nova amostra dos dados para criar um novo conjunto de dados que represente melhor o destino.  
  
 Criar o tipo certo de dados para treinar e testar seus modelos é uma parte importante da mineração de dados, mas também é uma parte que pode ser tediosa sem as ferramentas corretas. O assistente executa a amostragem estratificada para garantir que os conjuntos de treinamento e teste são bem equilibrados.  
  
## <a name="random-sampling-and-oversampling"></a>Amostragem e sobreamostragem aleatórias  
 . A amostragem aleatória é a melhor maneira de assegurar que os dados usados para testar um modelo representem razoavelmente os dados usados para criar o modelo. Você pode criar aleatoriamente dados de exemplo armazenados no Excel ou em uma fonte de dados externa.  
  
 Se você usar a opção de amostragem aleatória, o **dados de exemplo** assistente automaticamente cria conjuntos de dados de treinamento e teste e incluirá em planilhas separadas do Excel para referência posterior.  
  
 Se seus dados são armazenados em uma pasta de trabalho do Excel e não uma fonte de dados externa, você também tem a opção de usar *sobreamostragem*. Com essa opção, você especifica um valor de destino que pode ser escasso nos seus dados, e o assistente coletará um conjunto balanceado que inclui mais do valor de destino. Você pode instruir o assistente a atingir uma porcentagem de destino ou criar um certo número de linhas.  
  
 Se você usar a opção de sobreamostragem, o **dados de exemplo** assistente cria uma nova planilha que contém os dados de exemplo recém-balanceados.  
  
## <a name="using-the-sample-data-wizard"></a>Usando o Assistente de Dados de Amostra  
  
#### <a name="to-separate-data-into-training-and-testing-sets"></a>Para separar dados em conjuntos de treinamento e de teste  
  
1.  No **Data Mining** faixa de opções, clique em **dados de exemplo**.  
  
2.  Sobre o **Selecionar fonte de dados** , especifique se o **dados** que você deseja particionar estão em um intervalo do Excel ou uma tabela ou em uma fonte de dados externa.  
  
3.  Sobre o **Selecionar tipo de amostragem** , especifique se deseja criar o treinamento e conjuntos de dados de teste por amostragem aleatória ou criar um novo conjunto de dados por sobreamostragem.  
  
    > [!NOTE]  
    >  Se você estiver usando uma fonte de dados externa, apenas a opção de amostragem aleatória estará disponível. Se você desejar usar a sobreamostragem com dados externos, poderá importar os dados para uma pasta de trabalho do Excel usando uma conexão de dados do Excel e, depois, usar o Assistente de Dados de Exemplo.  
  
4.  Defina as opções específicas ao método de amostragem selecionado.  
  
    -   Para a amostragem aleatória, especifique uma porcentagem dos dados originais para uso em testes ou o número total de linhas para uso no conjunto de dados de teste.  
  
    -   Para a sobreamostragem, selecione a coluna e o valor que você deseja enfatizar. Em seguida, especifique o número total de linhas no novo conjunto de dados e a porcentagem de linhas no novo conjunto de dados que devem incluir o valor de destino.  
  
         O valor de destino da sobreamostragem deve ser um valor discreto; você não pode fazer a sobreamostragem de dados numéricos contínuos.  
  
5.  Sobre o **página concluir**, aceite os nomes padrão para novos conjuntos de dados ou digite um novo nome.  
  
     O assistente cria novas planilhas para cada conjunto de dados.  
  
 A maioria dos assistentes no Cliente de Mineração de Dados para Excel também fornece uma opção para separar aleatoriamente os dados em conjuntos de treinamento e teste. No entanto, se você usar os assistentes, os dados permanecerão na mesma planilha (ou em outra fonte de dados), e as informações que determinam se uma linha é um caso de teste ou de treinamento serão armazenadas internamente. Por outro lado, quando você usa o **dados de exemplo** assistente, o teste e os dados de treinamento são incluídos em planilhas separadas para facilitar a referência.  
  
## <a name="related-options"></a>Opções relacionadas  
 À medida que você percorrer as etapas do assistente, terá as seguintes opções:  
  
|Opções|Comentários|  
|-------------|--------------|  
|Caixa de diálogo Selecionar Fonte de Dados (Cliente de Mineração de Dados para Excel)|Selecione um intervalo ou uma tabela do Excel que contém os dados. Se quiser usar dados externos, os dados poderão ser relacionais, mas devem ser incluídos em uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. T|  
|Página Selecionar Tipo de Amostragem (Cliente de Mineração de Dados para Excel)|Se você utilizar uma fonte de dados externa, ficará limitado ao uso da opção de amostragem aleatória. Além disso, você deve especificar o número de linhas a serem criadas no conjunto de dados final, usando o **contagem de linhas** opção. Não é possível especificar uma porcentagem dos dados de origem.|  
|Página amostragem aleatória (Cliente de Mineração de Dados para Excel)|Você pode copiar uma porcentagem de linhas da origem ou um número específico de linhas.|  
|Página de sobreamostragem (Cliente de Mineração de Dados para Excel)|**Estado de destino**<br /><br /> Selecione um valor na lista que esteja sub-representado no conjunto de dados original. A sobreamostragem aumentará a proporção de linhas de dados que incluem esse estado.<br /><br /> **Tamanho da amostra**<br /><br /> Selecione o número total de linhas a serem extraídas. Esse valor representa o tamanho do conjunto de dados final.|  
  
## <a name="other-sampling-options"></a>Outras opções de amostragem  
 Se as opções de amostragem nesse assistente não atenderem às suas necessidades, use a transformação de amostragem no SQL Server Integration Services (SSIS) para criar amostras de linhas de várias fontes de dados.  
  
 Para obter mais informações, consulte [Row Sampling Transformation](../integration-services/data-flow/transformations/row-sampling-transformation.md) e [transformação amostragem percentual](../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Lista de verificação de preparação para mineração de dados](checklist-of-preparation-for-data-mining.md)  
  
  
