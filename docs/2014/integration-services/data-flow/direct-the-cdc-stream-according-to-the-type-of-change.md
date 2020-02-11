---
title: Direcionar o fluxo de CDC de acordo com o tipo de alteração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3afa531e-f425-40a4-a1bf-1c3e1727287e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2ee2b3238a66000546619815a886fc6017c51fe6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62827393"
---
# <a name="direct-the-cdc-stream-according-to-the-type-of-change"></a>Direcionar o fluxo de CDC de acordo com o tipo de alteração
  Para adicionar e configurar uma Transformação de separador de CDC, o pacote deverá conter pelo menos uma tarefa de Fluxo de Dados e uma origem CDC.  
  
 A origem CDC adicionada ao pacote deve ter um modo de processamento NetCDC selecionado. Para obter mais informações sobre como selecionar modos de processamento, consulte [Editor de Origem CDC &#40;página Gerenciador de Conexões&#41;](../cdc-source-editor-connection-manager-page.md).  
  
### <a name="to-direct-the-cdc-stream-according-to-the-type-of-change"></a>Para direcionar o fluxo de CDC de acordo com o tipo de alteração  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste o separador de CDC para a superfície de design.  
  
4.  Conecte a origem CDC que é incluída no pacote ao Separador de CDC.  
  
5.  Conecte o separador de CDC a um ou mais destinos. Você pode conectar até três saídas diferentes.  
  
6.  Selecione uma das saídas a seguir:  
  
    -   Excluir saída: a saída para onde as linhas de alteração DELETE são direcionadas.  
  
    -   Inserir saída: a saída para onde as linhas de alteração INSERT são direcionadas.  
  
    -   Saída de atualização: a saída para onde as linhas de alteração UPDATE antes/depois e as linhas de alteração Mesclar são direcionadas.  
  
7.  Opcionalmente, você pode configurar as propriedades avançadas usando a caixa de diálogo **Editor Avançado** .  
  
     A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
     Para abrir a caixa de diálogo **Editor Avançado** :  
  
    -   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse no separador de CDC e selecione **Mostrar Editor Avançado**.  
  
     Para obter mais informações sobre como usar o separador de CDC, consulte Componentes de CDC para Microsoft SQL Server Integration Services.  
  
## <a name="see-also"></a>Consulte Também  
 [Divisor de CDC](cdc-splitter.md)  
  
  
