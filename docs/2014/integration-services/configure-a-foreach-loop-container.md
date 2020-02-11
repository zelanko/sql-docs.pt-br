---
title: Configurar um contêiner Loop Foreach | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Foreach Loop containers
- containers [Integration Services], Foreach Loop
ms.assetid: 519c6f96-5e1f-47d2-b96a-d49946948c25
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 461a652999e97907962486cfc05e5b6668f5590d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060882"
---
# <a name="configure-a-foreach-loop-container"></a>Para configurar um contêiner Loop Foreach
  Este procedimento descreve como configurar um contêiner Loop Foreach, incluindo expressões de propriedade nos níveis de enumerador e contêiner.  
  
### <a name="to-configure-the-foreach-loop-container"></a>Para configurar o contêiner Loop Foreach  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  Clique na guia **Fluxo de Controle** e clique duas vezes no Loop Foreach.  
  
3.  Na caixa de diálogo **Editor de Loop Foreach** , clique em **Geral** e, como alternativa, modifique o nome e a descrição do Loop Foreach.  
  
4.  Clique em **Coleção** e selecione um tipo de enumerador na lista **Enumerador** .  
  
5.  Especifique um enumerador e defina opções de enumerador conforme mostrado a seguir:  
  
    -   Para usar o enumerador de Arquivo Foreach, forneça a pasta que contém os arquivos a serem enumerados, especifique um filtro do nome e tipo de arquivo e especifique se o nome de arquivo totalmente qualificado deverá ser retornado. Indique também se você deseja a função recursiva em subpastas para obter mais arquivos.  
  
    -   Para usar o enumerador de Item Foreach, clique em **Colunas**e, na caixa de diálogo **Colunas Para Cada Item** , clique em **Adicionar** para adicionar colunas. Selecione um tipo de dados para cada coluna na lista **Tipo de Dados** e clique em **OK**.  
  
         Digite os valores nas colunas ou selecione-os nas listas.  
  
        > [!NOTE]  
        >  Para adicionar uma nova linha, clique em qualquer lugar fora da célula digitada.  
  
        > [!NOTE]  
        >  Se um valor não for compatível com o tipo de dados de coluna, o texto será realçado.  
  
    -   Para usar o enumerador ADO Foreach, selecione uma variável existente ou clique em **Nova Variável** na lista **Variável de origem de objeto ADO** para especificar a variável que contém o nome do objeto ADO a ser enumerado e selecione uma opção de modo de enumeração.  
  
         Se você estiver criando uma variável nova, defina as propriedades da variável na caixa de diálogo **Adicionar Variável** .  
  
    -   Para usar o enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach, selecione uma conexão ADO.NET existente ou clique em **Nova conexão** na lista **Conexão** e depois selecione um esquema.  
  
         Outra opção é clicar em **Definir Restrições** e selecionar restrições de esquema, selecionar a variável que contém o valor de restrição ou digitar o valor da restrição e clicar em **OK**.  
  
    -   Para usar o enumerador Foreach de Variável , selecione uma variável na lista **Variável** .  
  
    -   Para usar o enumerador NodeList Foreach, clique em DocumentSourceType, selecione o tipo de fonte na lista e clique em DocumentSource. Dependendo do valor selecionado para DocumentSourceType, selecione uma variável ou uma conexão de arquivo da lista, crie uma nova variável ou conexão de arquivo ou digite a origem XML no **Editor de Origem de Documento**.  
  
         Depois, clique em EnumerationType e selecione um tipo de enumeração na lista. Se EnumerationType for **Navegador, Nó ou Texto de Nó**, clique em OuterXPathStringSourceType e selecione o tipo de fonte, clicando em seguida em OuterXPathString. Dependendo do conjunto de valores de OuterXPathStringSourceType, selecione uma variável ou uma conexão de arquivo da lista, crie uma nova variável ou conexão de arquivo ou digite a cadeia de caracteres da expressão de XML Path Language (XPath) externa.  
  
         Se EnumerationType for **ElementCollection**,defina OuterXPathStringSourceType e OuterXPathString, conforme descrito acima. Depois, clique em InnerElementType e selecione um tipo de enumeração para os elementos internos e clique em InnerXPathStringSourceType. Dependendo do valor definido para InnerXPathStringSourceType, selecione uma variável ou uma conexão de arquivo, crie uma nova variável ou conexão de arquivo ou digite a cadeia de caracteres da expressão XPath interna.  
  
    -   Para usar o enumerador SMO Foreach, selecione uma conexão ADO.NET existente ou clique em **Nova conexão** na lista **Conexão** e então digite a cadeia de caracteres a ser usada ou clique em **Procurar**. Se você clicar em **Procurar**, na caixa de diálogo **Selecionar Enumeração SMO** , selecione o tipo de objeto a ser enumerado e o tipo de enumeração e clique em **OK**.  
  
6.  Outra opção é clicar no botão Procurar **(…)** na caixa de texto **Expressões** na página **Coleção** para criar expressões que atualizem os valores de propriedade. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](expressions/add-or-change-a-property-expression.md).  
  
    > [!NOTE]  
    >  As propriedades relacionadas na lista **Propriedade** variam por enumerador.  
  
7.  Opcionalmente, clique em **Mapeamentos de Variáveis** para mapear propriedades de objeto do valor da coleção e execute um dos procedimentos a seguir:  
  
    1.  Na lista **Variáveis**, selecione uma variável ou clique em **\<Nova Variável>** para criar uma nova variável.  
  
    2.  Se você adicionar uma variável nova, defina as propriedades da variável na caixa de diálogo **Adicionar Variável** e clique em **OK**.  
  
    3.  Se você usar o enumerador Para Cada Item, você poderá atualizar o valor de índice na lista **Índice** .  
  
        > [!NOTE]  
        >  O valor de índice indica qual coluna no item será mapeada para a variável. Apenas o enumerador Para Cada Item pode usar um valor de índice diferente de 0.  
  
8.  Opcionalmente, clique em **Expressões** e, na página **Expressões** , crie expressões de propriedade para as propriedades do contêiner Loop Foreach. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](expressions/add-or-change-a-property-expression.md).  
  
9. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Contêiner do Loop Foreach](control-flow/foreach-loop-container.md)  
  
  
