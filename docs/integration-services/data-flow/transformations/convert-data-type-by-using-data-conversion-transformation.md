---
title: "Converter dados em um tipo de dados diferente por meio da transforma&#231;&#227;o Convers&#227;o de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "convertendo tipos de dados [Integration Services]"
  - "transformação Conversão de Dados"
  - "tipos de dados [Integration Services], convertendo"
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Converter dados em um tipo de dados diferente por meio da transforma&#231;&#227;o Convers&#227;o de Dados
  Para adicionar e configurar uma transformação Conversão de Dados, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma fonte.  
  
### Para converte dados em um tipo de dados diferente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a transformação Conversão de Dados para a superfície de design.  
  
4.  Conecte a transformação Conversão de Dados ao fluxo de dados arrastando um conector de uma fonte ou transformação anterior para a transformação Conversão de Dados.  
  
5.  Clique duas vezes na transformação Conversão de Dados.  
  
6.  Na caixa de diálogo **Editor de Transformação Conversão de Dados**, na tabela **Colunas de Entrada Disponíveis**, marque a caixa de seleção ao lado das colunas das quais o tipo de dados você deseja converter.  
  
    > [!NOTE]  
    >  É possível aplicar diversas conversões de dados a uma coluna de entrada.  
  
7.  Como opção, modifique os valores padrão na coluna **Alias de Saída**.  
  
8.  Na lista **Tipo de Dados**, selecione o novo tipo de dados para a coluna. O tipo de dados padrão é o tipo de dados da coluna de entrada.  
  
9. Como opção, dependendo do tipo de dados selecionado, atualize os valores nas colunas **Comprimento**, **Precisão**, **Escala** e **Página de Código**.  
  
10. Para configurar a saída de erro, clique em **Configurar Saída de Erro**. Para obter mais informações, consulte [Configurar uma saída de erro em um componente de fluxo de dados](../../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md).  
  
11. Clique em **OK**.  
  
12. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## Consulte também  
 [Transformação Conversão de Dados](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tipos de dados do Integration Services](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Tarefa de Fluxo de Dados](../../../integration-services/control-flow/data-flow-task.md)  
  
  