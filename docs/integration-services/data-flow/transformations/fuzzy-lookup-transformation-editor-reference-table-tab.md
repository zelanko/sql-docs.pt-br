---
title: "Editor de Transforma&#231;&#227;o Pesquisa Difusa (guia Tabela de Refer&#234;ncia) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzylookuptransformation.referencetable.f1"
helpviewer_keywords: 
  - "Editor de Transformação Pesquisa Difusa"
ms.assetid: 451f4e7d-1c8e-4784-b540-df0806509bf1
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Editor de Transforma&#231;&#227;o Pesquisa Difusa (guia Tabela de Refer&#234;ncia)
  Use a guia **Tabela de Referência** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para especificar a tabela de origem e o índice a ser usado na pesquisa. A fonte de dados de referência deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  A transformação Pesquisa Difusa cria uma cópia de trabalho da tabela de referência. Os índices descritos abaixo são criados nesta tabela de trabalho usando uma tabela especial, não um índice do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comum. A transformação não modifica as tabelas de origem existentes a menos que você selecione **Manter índice armazenado**. Nesse caso, ela cria um gatilho na tabela de referência que atualiza a tabela de trabalho e a tabela de índices de pesquisa baseada em alterações na tabela de referência.  
  
> [!NOTE]  
>  As propriedades **Exhaustive** e **MaxMemoryUsage** da transformação Pesquisa Difusa não estão disponíveis no **Editor de Transformação Pesquisa Difusa**, mas podem ser definidas por meio do **Editor Avançado**. Além disso, um valor acima de 100 para **MaxOutputMatchesPerInput** só pode ser especificado no **Editor Avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Transformação de Pesquisa Difusa em [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Para saber mais sobre a transformação Pesquisa Difusa, consulte [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
## Opções  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB**.  
  
 **Gerar novo índice**  
 Especifique que a transformação deve criar um índice novo para ser utilizado na pesquisa.  
  
 **Nome da tabela de referência**  
 Selecione a tabela existente para usar como tabela de referência (pesquisa).  
  
 **Armazenar novo índice**  
 Selecione esta opção para salvar o novo índice de pesquisa.  
  
 **Novo nome de índice**  
 Se você optou por salvar o novo índice de pesquisa, digite um nome descritivo para o índice.  
  
 **Manter índice armazenado**  
 Se você optou por salvar o novo índice de pesquisa, especifique se deseja que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mantenha o índice.  
  
> [!NOTE]  
>  Quando você seleciona **Manter índice armazenado** na guia **Tabela de Referência** de **Editor de Transformação Pesquisa Difusa**, a transformação usa procedimentos armazenados gerenciados para manter o índice. Esses procedimentos armazenados gerenciados usam o recurso de integração de CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, a integração de CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não está habilitada. Para usar a funcionalidade **Manter índice armazenado** , você deve habilitar a integração de CLR. Para obter mais informações, consulte [Enabling CLR Integration](../Topic/Enabling%20CLR%20Integration.md).  
>   
>  Como a opção **Manter índice armazenado** requer a integração CLR, esse recurso só funciona quando você seleciona uma tabela de referência em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde a integração CLR está habilitada.  
  
 **Usar índice já existente**  
 Especifique que a transformação deve usar um índice existente na pesquisa.  
  
 **Nome de um índice já existente**  
 Selecione um índice de pesquisa criado anteriormente na lista.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Pesquisa Difusa &#40;guia Colunas&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Avançado&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  