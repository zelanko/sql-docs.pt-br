---
title: Caixa de diálogo de propriedades do visor, centro e Zoom do mapa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.centerandzoom.f1
- "10506"
ms.assetid: 642a06f5-293f-48e0-97a6-1489dbefa719
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a5c71344fe45df4265db72e9fd6dc41ac13bd98
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108287"
---
# <a name="map-viewport-properties-dialog-box-center-and-zoom"></a>Caixa de diálogo Propriedades do Visor do Mapa, Centro e Zoom
  Selecione **Centralizar e Aplicar Zoom** para a caixa de diálogo **Propriedades do Visor do Mapa** para definir a exibição central e o fator de zoom de um mapa. Depois que você especificar uma fonte de dados do mapa e os limites do mapa a serem incluídos em seu relatório, poderá especificar o centro de exibição e o fator de zoom para controlar ainda mais a exibição do mapa. As opções são alteradas de acordo com o método usado para especificar os valores de centro e zoom. Clique no botão **Expressão** (*fx*) para editar uma expressão que define o valor da opção.  
  
## <a name="options"></a>Opções  
 **Definir um centro de exibição e o nível de zoom**  
 Escolha esta opção para especificar valores personalizados para o centro de exibição e o nível de zoom.  
  
 **Centralizar mapa para mostrar uma camada do mapa**  
 Escolha esta opção para especificar uma camada e centralizar automaticamente a exibição em seus dados de mapa. Por exemplo, centralize a exibição em LineLayer1.  
  
 **Centralizar mapa para mostrar um elemento de mapa inserido**  
 Escolha esta opção para centralizar a exibição em um elemento do mapa com ligação de dados específico. Os dados espaciais devem ter uma relação com os dados analíticos para especificar essa opção.  
  
 Por exemplo, centralize a exibição no elemento do mapa em que o nome do campo de correspondência é [Cidade] e o valor de correspondência é "Seattle".  
  
 **Centralizar mapa para mostrar todos os elementos do mapa com ligação de dados**  
 Escolha esta opção para centralizar a exibição em todos os elementos do mapa na camada. Os dados espaciais devem ter uma relação com os dados analíticos para especificar essa opção.  
  
 Por exemplo, centralize a exibição na camada de bolha do polígono que mostra cidades e o tamanho da bolha está relacionado a população. Somente as cidades com um valor de população correspondente são incluídos durante o cálculo do centro para o visor.  
  
 **Opções de centralização e zoom**  
 Selecione uma opção para especificar o centro de exibição e o nível de zoom.  
  
 **Exibir X central () %**  
 A coordenada horizontal. O valor padrão, 50%. centraliza a exibição no ponto médio entre os valores mínimo e máximo.  
  
 **Exibir Y central () %**  
 A coordenada vertical. O valor padrão, 50%. centraliza a exibição no ponto médio entre os valores verticais mínimo e máximo.  
  
 **Nível de zoom (%)**  
 O fator de zoom. O valor padrão, 100%, indica que não há nenhuma ampliação.  
  
 **Centralizar exibição nesta camada**  
 Especifique o nome da camada.  
  
 **Centralizar exibição no elemento do mapa que corresponde a esta condição**  
 O campo somente leitura exibido é usado para corresponder a dados do mapa e dados analíticos. Especifique o valor que você deseja corresponder. A exibição é centralizada automaticamente neste elemento do mapa. Por exemplo, NAME = TEXAS. Por padrão, o tipo de dados para a condição é String e a correspondência faz distinção entre maiúsculas e minúsculas.  
  
 Para corresponder em um campo que tenha um tipo de dados diferente, você deve escrever uma expressão que seja avaliada para esse tipo de dados. Por exemplo, se o campo de correspondência for um código postal de 5 dígitos armazenado como um número inteiro, para especificar o código postal 98053, você deve usar a expressão = 98053.  
  
## <a name="see-also"></a>Consulte também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
