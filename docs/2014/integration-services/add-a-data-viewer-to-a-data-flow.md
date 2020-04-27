---
title: Adicionar um visualizador de dados a um fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data viewers [Integration Services]
- data flow [Integration Services], data viewers
- adding data viewers
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cbd45caac75d4fac3b5fffc305a9f359193191a5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062091"
---
# <a name="add-a-data-viewer-to-a-data-flow"></a>Adicionar um visualizador de dados a um fluxo de dados
  Este tópico descreve como adicionar e configurar um visualizador de dados em um fluxo de dados. Um visualizador de dados exibe dados que estão se movendo entre dois componentes de fluxo de dados. Por exemplo, um visualizador de dados pode exibir os dados extraídos de uma fonte antes de uma transformação no fluxo de dados modificar os dados.  
  
 Um caminho conecta componentes em um fluxo de dados conectando a saída de um componente de fluxo de dados à entrada de outro componente.  
  
 Antes de adicionar visualizadores de dados, um pacote deve incluir uma tarefa Fluxo de Dados e pelo menos dois componentes de fluxo de dados que estejam conectados.  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>Para adicionar um visualizador de dados a um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** , se ainda não estiver ativada.  
  
4.  Clique na tarefa Fluxo de Dados do fluxo de dados ao qual você deseja conectar um visualizador de dados e, em seguida, clique na guia **Fluxo de Dados** .  
  
5.  Clique com o botão direito do mouse em um caminho entre dois componentes de fluxo de dados e clique em **Editar**.  
  
6.  Na página **Geral** , você pode exibir e editar propriedades do caminho. Por exemplo, na lista suspensa **PathAnnotation** , você pode selecionar a anotação que aparece ao lado do caminho.  
  
7.  Na página **Metadados** , você pode exibir os metadados da coluna e copiar os metadados na Área de Transferência.  
  
8.  Na página **Visualizador de Dados** , clique em **Habilitar visualizador de dados**.  
  
9. Na área Colunas para exibição, selecione as colunas a serem exibidas no visualizador de dados. Por padrão, todas as colunas disponíveis são selecionadas e relacionadas na lista **Colunas Exibidas** . Mova as colunas que não deseja usar para a lista **Coluna Não Usada** selecionando-as e clicando na seta para a esquerda.  
  
    > [!NOTE]  
    >  Na grade, os valores que representam os tipos de dados DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET aparecem como cadeias de caracteres formatadas conforme o ISO 8601 e um separador de espaço substitui o separador `T`. Os valores que representam os tipos de dados DT_DATE e DT_FILETIME incluem sete dígitos para os segundos fracionários. Como o tipo de dados DT_FILETIME armazena somente três dígitos de segundos fracionários, a grade exibe zeros nos quatro dígitos restantes. Os valores que representam o tipo de dados DT_DBTIMESTAMP incluem três dígitos para os segundos fracionários. Para os valores que representam os tipos de dados DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, o número de dígitos para os segundos fracionários corresponde à escala especificada para o tipo de dados da coluna. Para obter mais informações sobre os formatos ISO 8601, consulte [Formatos de data e hora](../../2014/integration-services/date-and-time-formats.md). Para obter mais informações sobre tipos de dados, consulte [Integration Services tipos de dados](data-flow/integration-services-data-types.md).  
  
10. Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Transformações de Integration Services](data-flow/transformations/integration-services-transformations.md)   
 [Caminhos de Integration Services](data-flow/integration-services-paths.md)   
 [Fluxo de dados](data-flow/data-flow.md)   
 [Depurar o fluxo de dados](troubleshooting/debugging-data-flow.md)  
  
  
