---
title: "Adicionar um visualizador de dados a um fluxo de dados | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "visualizadores de dados [Integration Services]"
  - "fluxo de dados [Integration Services], visualizadores de dados"
  - "adicionando visualizadores de dados"
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Adicionar um visualizador de dados a um fluxo de dados
  Este tópico descreve como adicionar e configurar um visualizador de dados em um fluxo de dados. Um visualizador de dados exibe dados que estão se movendo entre dois componentes de fluxo de dados. Por exemplo, um visualizador de dados pode exibir os dados extraídos de uma fonte antes de uma transformação no fluxo de dados modificar os dados.  
  
 Um caminho conecta componentes em um fluxo de dados conectando a saída de um componente de fluxo de dados à entrada de outro componente.  
  
 Antes de adicionar visualizadores de dados, um pacote deve incluir uma tarefa Fluxo de Dados e pelo menos dois componentes de fluxo de dados que estejam conectados.  
  
 Adicione um visualizador de dados a uma saída de erro para ver a descrição do erro e o nome da coluna na qual ocorreu o erro. Por padrão, a saída de erro inclui somente identificadores numéricos para o erro e a coluna.  
  
### Para adicionar um visualizador de dados a um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle**, se ainda não estiver ativada.  
  
4.  Clique na tarefa Fluxo de Dados do fluxo de dados ao qual você deseja conectar um visualizador de dados e, em seguida, clique na guia **Fluxo de Dados**.  
  
5.  Clique com o botão direito do mouse em um caminho entre dois componentes de fluxo de dados e clique em **Editar**.  
  
6.  Na página **Geral**, você pode exibir e editar propriedades do caminho. Por exemplo, na lista suspensa **PathAnnotation**, você pode selecionar a anotação que aparece ao lado do caminho.  
  
7.  Na página **Metadados**, você pode exibir os metadados da coluna e copiar os metadados na Área de Transferência.  
  
8.  Na página **Visualizador de Dados**, clique em **Habilitar visualizador de dados**.  
  
9. Na área Colunas para exibição, selecione as colunas a serem exibidas no visualizador de dados. Por padrão, todas as colunas disponíveis são selecionadas e relacionadas na lista **Colunas Exibidas**. Mova as colunas que não deseja usar para a lista **Coluna Não Usada** selecionando-as e clicando na seta para a esquerda.  
  
    > [!NOTE]  
    >  Na grade, os valores que representam os tipos de dados DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET aparecem como cadeias de caracteres formatadas conforme o ISO 8601 e um separador de espaço substitui o separador **T**. Os valores que representam os tipos de dados DT_DATE e DT_FILETIME incluem sete dígitos para os segundos fracionários. Como o tipo de dados DT_FILETIME armazena somente três dígitos de segundos fracionários, a grade exibe zeros nos quatro dígitos restantes. Os valores que representam o tipo de dados DT_DBTIMESTAMP incluem três dígitos para os segundos fracionários. Para os valores que representam os tipos de dados DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, o número de dígitos para os segundos fracionários corresponde à escala especificada para o tipo de dados da coluna. Para obter mais informações sobre os formatos ISO 8601, consulte [Formatos de data e hora](../Topic/Date%20and%20Time%20Formats.md). Para obter mais informações sobre tipos de dados, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
10. Clique em **OK**.  
  
## Consulte também  
 [Transformações do Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../integration-services/data-flow/integration-services-paths.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)   
 [Depurando fluxo de dados](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
  