---
title: Transformação Mapa de Caracteres | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactertrans.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d00f864d5e7209bc0865bfbb52bd1231a2c12a9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770410"
---
# <a name="character-map-transformation"></a>Transformação Mapas de Caracteres
  A transformação Mapa de Caracteres aplica funções de cadeia de caracteres, como a conversão de letra minúscula em maiúscula, em dados de caracteres. Essa transformação funciona apenas em dados de coluna com um tipo de dados de cadeia de caracteres.  
  
 A transformação Mapa de Caracteres pode converter dados de coluna existentes ou adicionar uma coluna à saída de transformação e colocar os dados convertidos na coluna nova. Você pode aplicar conjuntos diferentes de operações de mapeamento na mesma coluna de entrada e colocar os resultados em colunas diferentes. Por exemplo, é possível converter a mesma coluna em maiúsculas e minúsculas e colocar os resultados em duas colunas diferentes.  
  
 O mapeamento pode, em algumas circunstâncias, fazer com que os dados fiquem truncados. Por exemplo, o truncamento pode acontecer quando caracteres de byte único são mapeados para caracteres com representação de vários bytes. A transformação Mapa de Caracteres inclui uma saída de erro, que pode ser usada para direcionar dados truncados para uma saída separada. Para obter mais informações, consulte [Tratamento de erros em dados](../error-handling-in-data.md).  
  
 Essa transformação tem uma entrada, uma saída e uma saída de erro.  
  
## <a name="mapping-operations"></a>Mapeando operações  
 A tabela a seguir descreve as operações de mapeamento suportadas pela transformação Mapa de Caracteres.  
  
|Operação|Descrição|  
|---------------|-----------------|  
|Inversão de bytes|Inverte a ordem de bytes.|  
|Largura inteira|Mapeia caracteres de meia largura para caracteres de largura inteira.|  
|Meia largura|Mapeia caracteres de largura inteira para caracteres de meia largura.|  
|Hiragana|Mapeia caracteres katakana para caracteres hiragana.|  
|Katakana|Mapeia caracteres hiragana para caracteres katakana.|  
|Caixas linguísticas|Aplica caixas linguísticas em vez de regras do sistema. As caixas linguísticas se referem à funcionalidade fornecida pela API do Win32 para mapeamento de maiúsculas/minúsculas simples de Unicode de idiomas turcomanos e de outras localidades.|  
|Minúscula|Converte caracteres em minúsculas.|  
|Chinês simplificado|Mapeia caracteres de chinês tradicional para caracteres de chinês simplificado.|  
|Chinês tradicional|Mapeia caracteres de chinês simplificado para caracteres de chinês tradicional.|  
|Letras Maiúsculas|Converte caracteres em maiúsculas.|  
  
## <a name="mutually-exclusive-mapping-operations"></a>Operações de mapeamento mutuamente exclusivas  
 Mais de uma operação pode ser executada em uma transformação. Entretanto, algumas operações de mapeamento são mutuamente exclusivas. A tabela a seguir relaciona restrições que se aplicam quando você usa várias operações na mesma coluna. As operações nas colunas Operação A e Operação B são mutuamente exclusivas.  
  
|Operação A|Operação B|  
|-----------------|-----------------|  
|Minúscula|Letras Maiúsculas|  
|Hiragana|Katakana|  
|Meia largura|Largura inteira|  
|Chinês tradicional|Chinês simplificado|  
|Minúscula|Hiragana, katakana, meia largura, largura inteira|  
|Letras Maiúsculas|Hiragana, katakana, meia largura, largura inteira|  
  
## <a name="configuration-of-the-character-map-transformation"></a>Configuração da transformação Mapa de Caracteres  
 Você pode configurar a transformação Mapa de Caracteres das seguintes formas:  
  
-   Especificando as colunas a serem convertidas.  
  
-   Especificando as operações a serem aplicadas em cada coluna.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação de Mapas de Caracteres** , consulte [Character Map Transformation Editor](../../character-map-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  
