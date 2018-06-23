---
title: Transformação Dinâmica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ed9e181d9e346e39aa537b50fa8c0b166ba03da1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121316"
---
# <a name="pivot-transformation"></a>transformação Dinâmica
  A transformação Dinâmica transforma um conjunto de dados normalizado em um conjunto menos normalizado, em uma versão mais compacta, tornando dinâmicos os dados de entrada em um valor de coluna. Por exemplo, um conjunto de dados **Orders** normalizado que lista nome de cliente, produto e quantidade adquirida normalmente tem várias linhas para qualquer cliente que tenha comprado diversos produtos, sendo que cada linha daquele cliente apresenta detalhes do pedido para um produto diferente. Ao dinamizar o conjunto de dados na coluna de produto, a transformação dinâmica pode produzir um conjunto de dados com uma única linha por cliente. Aquela única linha lista todas as compras realizadas pelo cliente, com os nomes de produto mostrados como nomes de coluna, e a quantidade exibida como um valor na coluna de produto. Como nem todo cliente compra todos os produtos, muitas colunas podem conter valores nulos.  
  
 Quando um conjunto de dados é dinamizado, as colunas de entrada executam funções diferentes no processo de dinamização. Uma coluna pode participar dos seguintes modos:  
  
-   A coluna é passada inalterada até a saída. Como muitas linhas de entrada só podem resultar em uma linha de saída, a transformação copia só o primeiro valor de entrada para a coluna.  
  
-   A coluna age como a chave ou parte da chave que identifica um conjunto de registros.  
  
-   A coluna define a dinamização. Os valores nesta coluna são associados com colunas no conjunto de dados dinâmicos.  
  
-   A coluna contém valores que são colocados nas colunas criadas pela dinamização.  
  
 Essa transformação tem uma entrada, uma saída comum e uma saída de erro.  
  
## <a name="sort-and-duplicate-rows"></a>Classificar e duplicar linhas  
 Para dinamizar os dados com eficiência, o que significa criar o mínimo possível de registros no conjunto de dados de saída, os dados de entrada devem ser classificados na coluna dinâmica. Se os dados não fossem classificados, a transformação dinâmica poderia gerar vários registros para cada valor na chave definida, que é a coluna que define a associação de conjunto. Por exemplo, se um conjunto de dados fosse dinamizado em uma coluna **Name** , mas os nomes não fossem classificados, o conjunto de dados de saída poderia ter mais de uma linha para cada cliente, porque uma dinamização ocorre toda vez que o valor **Name** é alterado.  
  
 Os dados de entrada poderiam conter linhas duplicadas que causarão uma falha na transformação dinâmica. "Linhas duplicadas" significam linhas que têm os mesmos valores nas colunas de chave definidas e nas colunas dinâmicas. Para evitar uma falha, você pode configurar a transformação para redirecionar linhas de erro para uma saída de erro ou pode pré-agregar valores para ter certeza de que não existem linhas duplicadas.  
  
##  <a name="options"></a> Opções da caixa de diálogo Dinâmica  
 Você configura a operação dinâmica definindo as opções na caixa de diálogo **Dinâmica** . Para abrir a caixa de diálogo **Dinâmica** , adicione a transformação Dinâmica ao pacote no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]e clique com o botão direito do mouse no componente e clique em **Editar**.  
  
 A lista a seguir descreve as opções da caixa de diálogo **Dinâmica** .  
  
 **Chave Dinâmica**  
 Especifica a coluna a ser usada para obter valores na linha superior (linha de cabeçalho) da tabela.  
  
 **Definir Chave**  
 Especifica a coluna a ser usada para obter valores na coluna esquerda da tabela. A data de entrada deve ser classificada nesta coluna.  
  
 **Valor Dinâmico**  
 Especifica a coluna a ser usada para obter os valores da tabela, que não sejam os valores da linha do cabeçalho e da coluna esquerda.  
  
 **Ignorar valores de Chave Dinâmica não correspondentes e relatá-los após a execução de DataFlow**  
 Selecione essa opção para configurar a transformação Dinâmica para ignorar as linhas que contêm valores não reconhecidos na coluna **Chave Dinâmica** e gerar todos os valores de chave dinâmica para uma mensagem de log, quando o pacote é executado.  
  
 Você também pode configurar a transformação para gerar os valores definindo a propriedade personalizada `PassThroughUnmatchedPivotKeys` como `True`.  
  
 **Gerar colunas de saída dinâmica a partir de valores**  
 Digite os valores de chave dinâmica nesta caixa para permitir que a transformação Dinâmica crie colunas de saída para cada valor. Você pode inserir os valores antes de executar o pacote ou fazer o seguinte:  
  
1.  Selecione a opção **Ignorar valores de Chave Dinâmica não correspondentes e relatá-los após a execução de DataFlow** e clique em **OK** na caixa de diálogo **Dinâmica** para salvar as alterações à transformação Dinâmica.  
  
2.  Execute o pacote.  
  
3.  Quando o pacote tiver êxito, clique na guia **Progresso** e procure a mensagem de log de informações da transformação Dinâmica que contém os valores de chave dinâmica.  
  
4.  Clique com o botão direito do mouse na mensagem e clique em **Copiar Texto de Mensagem**.  
  
5.  Clique em **Parar Depuração** no menu **Depurar** para alternar para o modo de design.  
  
6.  Clique com o botão direito do mouse na transformação Dinâmica e clique em **Editar**.  
  
7.  Desmarque a opção **Ignorar valores de Chave Dinâmica não correspondentes e relatá-los após a execução de DataFlow** e cole os valores de chave dinâmica na caixa de diálogo **Gerar colunas de saída dinâmicas a partir dos valores** usando o formato a seguir.  
  
     [valor1],[valor2],[valor3]  
  
 **Gerar Colunas Agora**  
 Clique para criar uma coluna de saída para cada valor de chave dinâmica listada na caixa **Gerar colunas de saída dinâmicas a partir dos valores** .  
  
 As colunas de saída aparecem na caixa **Colunas de saída dinâmicas existentes** .  
  
 **Colunas de saída dinâmicas existentes**  
 Lista as colunas de saída para os valores de chave dinâmica.  
  
 A tabela a seguir mostra um conjunto de dados após a dinamização dos dados na coluna **Ano** .  
  
|Ano|Nome do produto|Total|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Tubo de pneu de estrada|35920.50|  
|2004|Garrafa de Água – 30 oz.|2805.00|  
|2002|Pneu de Passeio|62364.225|  
  
 A tabela a seguir mostra um conjunto de dados depois de os dados serem dinamizados na coluna **Ano** .  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Tubo de pneu de estrada|3592.05|35920.50|89801.25|  
|Garrafa de Água – 30 oz.|*NULL*|*NULL*|2805.00|  
|Pneu de Passeio|62364.225|375051.60|1041810.00|  
  
 Para dinamizar os dados na coluna **Ano** , como mostrado acima, as opções a seguir são definidas na caixa de diálogo **Dinâmica** .  
  
-   Ano é selecionado na caixa de listagem **Chave Dinâmica** .  
  
-   O nome do produto é selecionado na caixa de listagem **Definir Chave** .  
  
-   Total é selecionado na caixa de listagem **Valor Dinâmico** .  
  
-   Os valores a seguir são inseridos na caixa **Gerar colunas de saída dinâmicas a partir dos valores** .  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>Configuração da Transformação Dinâmica  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** , clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Para obter informações sobre como definir as propriedades desse componente, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transformação não dinâmica](pivot-transformation.md)   
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  