---
title: Transformação Conversão de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1573167bfe50e5dcb63734a90c7b9b5bd00e40a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297964"
---
# <a name="data-conversion-transformation"></a>transformação Conversão de Dados

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A transformação Conversão de Dados converte os dados de uma coluna de entrada em um tipo diferente de dados e os copia em uma nova coluna de saída. Por exemplo, um pacote pode extrair dados de várias fontes e usar essa transformação para converter colunas em tipos de dados exigidos pelo armazenamento dos dados de destino. Você pode aplicar várias conversões em uma única coluna de entrada.  
  
 Usando essa transformação, um pacote pode executar os seguintes tipos de conversão de dados:  
  
-   Alterar o tipo de dados. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
    > [!NOTE]  
    >  Se você estiver convertendo dados em um tipo de dados de data ou data/hora, a data na coluna de saída estará no formato ISO, embora a preferência de localidade possa especificar um formato diferente.  
  
-   Defina o comprimento da coluna dos dados da cadeia de caracteres e a precisão e a escala em dados numéricos. Para obter mais informações, consulte [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
-   Especifique uma página de código. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
    > [!NOTE]  
    >  Ao copiar entre colunas com um tipo de dados de cadeia de caracteres, as duas colunas devem usar a mesma página de código.  
  
 Se o comprimento de uma coluna de saída de dados de cadeia de caracteres for menor do que o comprimento de sua coluna de entrada correspondente, os dados de saída serão truncados. Para obter mais informações, consulte [Tratamento de erros em dados](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente. Para obter informações sobre como usar a transformação Conversão de Dados no Designer SSIS, consulte [Converter dados em um tipo de dados diferente por meio da transformação Conversão de Dados](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md). Para obter informações sobre como definir as propriedades dessa transformação programaticamente, consulte [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) e [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [Comparação de desempenho entre as técnicas de conversão de tipo de dados no SSIS 2008](https://go.microsoft.com/fwlink/?LinkId=220823), em blogs.msdn.com.  
  
## <a name="data-conversion-transformation-editor"></a>Editor de Transformação Conversão de Dados
  Use a caixa de diálogo **Editor de Transformação Conversão de Dados** para selecionar as colunas a converter, selecionar o tipo de dados ao qual converter a coluna e definir atributos de conversão.  
  
> [!NOTE]  
>  A propriedade **FastParse** das colunas de saída da transformação Conversão de Dados não está disponível no **Editor de Transformação Conversão de Dados**, mas pode ser definida por meio do **Editor Avançado**. Para obter mais informações sobre essa propriedade, consulte a seção Transformação Conversão de Dados em [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Selecione as colunas a converter, utilizando as caixas de seleção. as seleções adicionam colunas de entrada à tabela abaixo.  
  
 **Coluna de Entrada**  
 Selecione colunas a converter na lista de colunas de entrada disponíveis. Suas seleções serão refletidas nas caixas de seleção marcadas acima.  
  
 **Alias de Saída**  
 Digite um alias para cada coluna nova. O padrão é **Copiar de** seguido do nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Tipo de Dados**  
 Selecione na lista um tipo de dados disponível. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Comprimento**  
 Defina o tamanho de coluna para dados de cadeia de caracteres.  
  
 **Precisão**  
 Defina a precisão para dados numéricos.  
  
 **Escala**  
 Defina a escala para dados numéricos.  
  
 **Página de código**  
 Selecione a página de código apropriada para colunas de tipo DT_STR.  
  
 **Configurar saída de erro**  
 Especifique como tratar erros de nível de linha usando a caixa de diálogo [Configurar Saída de Erro](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="see-also"></a>Consulte Também  
 [Análise rápida](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
