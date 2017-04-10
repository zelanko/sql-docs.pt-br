---
title: "Transforma&#231;&#227;o Coluna Derivada | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.derivedcolumntrans.f1"
helpviewer_keywords: 
  - "várias colunas derivadas"
  - "expressões [Integration Services], colunas derivadas"
  - "colunas derivadas"
  - "colunas [Integration Services], derivações"
  - "transformação Coluna Derivada"
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
caps.latest.revision: 60
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 60
---
# Transforma&#231;&#227;o Coluna Derivada
  A transformação Coluna Derivada cria novos valores de coluna aplicando expressões às colunas de entrada de transformação. Uma expressão pode conter qualquer combinação de variáveis, funções, operadores e colunas da entrada de transformação. O resultado pode ser adicionado como uma coluna nova ou adicionado a uma coluna existente como um valor de substituição. A transformação Coluna Derivada pode definir várias colunas derivadas, e qualquer variável ou coluna de entrada pode aparecer em várias expressões.  
  
 É possível usar essa transformação para executar as seguintes tarefas:  
  
-   Concatenar dados de colunas diferentes em uma coluna derivada. Por exemplo, você pode combinar valores das colunas **FirstName** e **LastName** em uma única coluna derivada chamada **FullName**usando a expressão `FirstName + " " + LastName`.  
  
-   Extrair caracteres de dados de cadeia de caracteres utilizando funções, como SUBSTRING, e armazenar o resultado em uma coluna derivada. Por exemplo, é possível extrair a inicial de uma pessoa da coluna **FirstName** utilizando a expressão `SUBSTRING(FirstName,1,1)`.  
  
-   Aplicar funções matemáticas a dados numéricos e armazenar o resultado em uma coluna derivada. Por exemplo, você pode alterar o comprimento e a precisão de uma coluna numérica, **SalesTax**, para um número com duas casas decimais utilizando a expressão `ROUND(SalesTax, 2)`.  
  
-   Criar expressões que comparam colunas de entrada e variáveis. Por exemplo, você pode comparar a variável **Version** com os dados na coluna **ProductVersion**e, dependendo do resultado da comparação, utilizar o valor de **Version** ou de **ProductVersion**utilizando a expressão `ProductVersion == @Version? ProductVersion : @Version`.  
  
-   Extrair partes de um valor de data e hora. Por exemplo, você pode usar as funções GETDATE e DATEPART para extrair o ano atual por meio da expressão `DATEPART("year",GETDATE())`.  
  
-   Converta cadeias de caracteres de dados em um formato específico usando uma expressão.  
  
## <a name="configuration-of-the-derived-column-transformation"></a>Configuração da transformação Coluna Derivada  
 Você pode configurar a transformação Coluna Derivada das seguintes maneiras:  
  
-   Forneça uma expressão para cada coluna de entrada ou coluna nova a ser alterada. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
    > [!NOTE]  
    >  Se uma expressão fizer referência a uma coluna de entrada substituída pela transformação Coluna Derivada, a expressão utilizará o valor original da coluna e não o valor derivado.  
  
-   Se estiver adicionando resultados às novas colunas e o tipo de dados for **string**, especifique uma página de código. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
 A transformação Coluna Derivada inclui a propriedade personalizada FriendlyExpression. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md)e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada, uma saída comum e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Coluna Derivada** , consulte [Editor de Transformação Colunas Derivadas](../../../integration-services/data-flow/transformations/derived-column-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
-   [Derivar valores de coluna por meio da transformação Coluna Derivada](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [Exemplos de expressões SSIS](http://go.microsoft.com/fwlink/?LinkId=220761), em social.technet.microsoft.com  
