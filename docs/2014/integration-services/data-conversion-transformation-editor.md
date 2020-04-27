---
title: Editor de transformação conversão de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- Data Conversion Transformation Editor
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5346c808c7d724ae630bb3dd25016a9977af363e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060049"
---
# <a name="data-conversion-transformation-editor"></a>Editor de Transformação Conversão de Dados
  Use a caixa de diálogo **Editor de Transformação Conversão de Dados** para selecionar as colunas a converter, selecionar o tipo de dados ao qual converter a coluna e definir atributos de conversão.  
  
> [!NOTE]  
>  A `FastParse` propriedade das colunas de saída da transformação conversão de dados não está disponível no **Editor de transformação conversão de dados**, mas pode ser definida usando o **Editor avançado**. Para obter mais informações sobre essa propriedade, consulte a seção Transformação Conversão de Dados em [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md).  
  
 Para saber mais sobre a transformação Conversão de Dados, consulte [Data Conversion Transformation](data-flow/transformations/data-conversion-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Selecione as colunas a converter, utilizando as caixas de seleção. as seleções adicionam colunas de entrada à tabela abaixo.  
  
 **Coluna de Entrada**  
 Selecione colunas a converter na lista de colunas de entrada disponíveis. Suas seleções serão refletidas nas caixas de seleção marcadas acima.  
  
 **Alias de saída**  
 Digite um alias para cada coluna nova. O padrão é `Copy of` seguido do nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Tipo de dados**  
 Selecione na lista um tipo de dados disponível. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
 **Comprimento**  
 Defina o tamanho de coluna para dados de cadeia de caracteres.  
  
 **Precisão**  
 Defina a precisão para dados numéricos.  
  
 **Escala**  
 Defina a escala para dados numéricos.  
  
 **Página de código**  
 Selecione a página de código apropriada para colunas de tipo DT_STR.  
  
 **Configurar saída de erro**  
 Especifique como tratar erros de nível de linha usando a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Converter dados em um tipo de dados diferente por meio da transformação Conversão de Dados](data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  
