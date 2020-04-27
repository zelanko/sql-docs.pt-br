---
title: Editor de transformação mapa de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- Character Map Transformation Editor
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76f2c5e517ca81ae667df3efa6ccd2f49384f090
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060979"
---
# <a name="character-map-transformation-editor"></a>Editor de Transformação Mapas de Caracteres
  Use a caixa de diálogo **Editor de Transformação Mapas de Caracteres** para selecionar as funções de cadeia de caracteres a serem aplicadas aos dados de coluna, bem como para especificar se o mapeamento é uma alteração in-loco ou se deve ser adicionado como uma nova coluna.  
  
 Para saber mais sobre transformação Mapa de Caracteres, consulte [Character Map Transformation](data-flow/transformations/character-map-transformation.md).  
  
## <a name="options"></a>Opções  
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
|Letras minúsculas|Converter para letras minúsculas.|  
|Letras Maiúsculas|Converter para letras maiúsculas.|  
|Inversão de bytes|Converter invertendo a ordem de bytes.|  
|Hiragana|Converter caracteres japoneses de katakana em hiragana.|  
|Katakana|Converter caracteres japoneses de hiragana em katakana.|  
|Meia largura|Converter caracteres de largura inteira em meia largura.|  
|Largura inteira|Converter caracteres de meia largura em largura inteira.|  
|Caixas linguísticas|Aplicar regras linguísticas de maiúsculas e minúsculas (mapeamento simples de maiúsculas e minúsculas Unicode para a Turquia e outras localidades), em vez das regras do sistema.|  
|Chinês simplificado|Converter caracteres do chinês tradicional em caracteres do chinês simplificado.|  
|Chinês tradicional|Converter caracteres do chinês simplificado em caracteres do chinês tradicional.|  
  
 **Alias de saída**  
 Digite um alias para cada coluna de saída. O padrão é **Copiar de** seguido do nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) para especificar opções de tratamento de erro para esta transformação.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
