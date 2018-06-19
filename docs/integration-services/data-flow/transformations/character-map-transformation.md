---
title: Transformação Mapa de Caracteres | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a6d60fcbff7a6878b757997b2ddec8ae16066b92
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403228"
---
# <a name="character-map-transformation"></a>Transformação Mapas de Caracteres
  A transformação Mapa de Caracteres aplica funções de cadeia de caracteres, como a conversão de letra minúscula em maiúscula, em dados de caracteres. Essa transformação funciona apenas em dados de coluna com um tipo de dados de cadeia de caracteres.  
  
 A transformação Mapa de Caracteres pode converter dados de coluna existentes ou adicionar uma coluna à saída de transformação e colocar os dados convertidos na coluna nova. Você pode aplicar conjuntos diferentes de operações de mapeamento na mesma coluna de entrada e colocar os resultados em colunas diferentes. Por exemplo, é possível converter a mesma coluna em maiúsculas e minúsculas e colocar os resultados em duas colunas diferentes.  
  
 O mapeamento pode, em algumas circunstâncias, fazer com que os dados fiquem truncados. Por exemplo, o truncamento pode acontecer quando caracteres de byte único são mapeados para caracteres com representação de vários bytes. A transformação Mapa de Caracteres inclui uma saída de erro, que pode ser usada para direcionar dados truncados para uma saída separada. Para obter mais informações, consulte [Tratamento de erros em dados](../../../integration-services/data-flow/error-handling-in-data.md).  
  
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
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>Editor de Transformação Mapas de Caracteres
  Use a caixa de diálogo **Editor de Transformação Mapas de Caracteres** para selecionar as funções de cadeia de caracteres a serem aplicadas aos dados de coluna, bem como para especificar se o mapeamento é uma alteração in-loco ou se deve ser adicionado como uma nova coluna.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Use as caixas de seleção para selecionar as colunas a transformar, utilizando funções de cadeia de caracteres. Suas seleções aparecem na tabela abaixo.  
  
 **Coluna de Entrada**  
 Exibir colunas de entrada selecionadas na tabela acima. Você também pode alterar ou remover uma seleção, por meio da lista de colunas de entrada disponíveis.  
  
 **Destino**  
 Especifique entre salvar os resultados das operações de cadeia de caracteres no local, usando a coluna existente, ou salvar os dados modificados como uma nova coluna.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Nova coluna|Salve os dados em uma nova coluna. Atribua o nome de coluna em **Alias de Saída**.|  
|Alteração no local|Salve os dados modificados na coluna existente.|  
  
 **Operação**  
 Selecione na lista as funções de cadeia de caracteres a aplicar aos dados da coluna.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Minúscula|Converter para letras minúsculas.|  
|Letras Maiúsculas|Converter para letras maiúsculas.|  
|Inversão de bytes|Converter invertendo a ordem de bytes.|  
|Hiragana|Converter caracteres japoneses de katakana em hiragana.|  
|Katakana|Converter caracteres japoneses de hiragana em katakana.|  
|Meia largura|Converter caracteres de largura inteira em meia largura.|  
|Largura inteira|Converter caracteres de meia largura em largura inteira.|  
|Caixas linguísticas|Aplicar regras linguísticas de maiúsculas e minúsculas (mapeamento simples de maiúsculas e minúsculas Unicode para a Turquia e outras localidades), em vez das regras do sistema.|  
|Chinês simplificado|Converter caracteres do chinês tradicional em caracteres do chinês simplificado.|  
|Chinês tradicional|Converter caracteres do chinês simplificado em caracteres do chinês tradicional.|  
  
 **Alias de Saída**  
 Digite um alias para cada coluna de saída. O padrão é **Copiar de** seguido do nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar opções de tratamento de erro para esta transformação.  
  
  
