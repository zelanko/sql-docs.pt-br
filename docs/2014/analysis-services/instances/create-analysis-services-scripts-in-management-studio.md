---
title: Criar scripts de Analysis Services no Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8e3cca216f7c2312b4e7b54f2236a5d1f7bafd9e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080107"
---
# <a name="create-analysis-services-scripts-in-management-studio"></a>Criar scripts do Analysis Services no Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inclui recursos de geração de script, modelos e editores que você pode usar para gerar scripts de objetos e tarefas do Analysis Services.  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>Gerar scripts de tarefas do Analysis Services no Management Studio  
 Para gerar scripts de tarefas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , é preciso clicar em uma das opções de Script em uma caixa de diálogo orientada por tarefas. Todas as caixas de diálogo usadas para executar tarefas, como fazer backup ou restaurar banco de dados, processar um objeto ou criar uma agregação, incluem uma opção de Script na parte superior da caixa de diálogo. Selecionar um dessas opções gera um script XMLA baseado nas informações e configurações da caixa de diálogo.  
  
 Por padrão, o script é gerado e inserido em um editor de consultas XMLA, mas você também pode expandir a lista de opções de Script para direcionar o script à Área de Transferência do Windows ou a um arquivo.  
  
#### <a name="to-script-an-analysis-services-task"></a>Para gerar scripts de uma tarefa do Analysis Services  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
2.  Clique com o botão direito do mouse em um banco de dados e clique em **Backup**. Essa ação abre a caixa de diálogo Banco de Dados de Backup. Especifique um nome de arquivo de backup e escolha as opções que você deseja para esse backup.  
  
3.  Clique em **Script** na parte superior da caixa de diálogo. O recurso Script faz parte de todas as caixas de diálogo baseadas em tarefas no Management Studio. Ele tem as seguintes opções: **Ação do Script para a Nova Janela de Consulta** para abrir a janela do editor de consultas, **Ação de Script no Arquivo** para salvar o script XMLA em um arquivo ou **Ação de Script na Área de Transferência** para salvar o script XMLA na Área de Transferência.  
  
     Observe que a opção **Ação de Script no Trabalho** listada como opção de script no Management Studio não tem suporte nos scripts do Analysis Services.  
  
4.  Se você selecionar a opção padrão, **Ação do Script para a Nova Janela de Consulta**, um script gerado será inserido em uma janela de consulta XMLA.  
  
     Agora você pode fechar a caixa de diálogo Banco de Dados de Backup e editar ou executar o script XMLA diretamente.  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>Gerar scripts de objetos do Analysis Services no Management Studio  
 Para gerar script de objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , é preciso clicar com o botão direito do mouse em um objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selecionar **Criar para**, **Alterar para**ou **Excluir para**. Cada uma dessas opções pode ser direcionada para uma janela ou um arquivo, mas independentemente de para onde o script será direcionado, será na forma de um script de DDL em um wrapper XMLA. Uma grande vantagem desses scripts é que eles podem ser executados em qualquer servidor para o qual forem direcionados. Além disso, os nomes nos scripts podem ser alterados e executados de forma iterativa para a criação, alteração ou exclusão em massa de objetos.  
  
 Os objetos para os quais você pode gerar script incluem os elementos de um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluindo fontes de dados, exibições de fontes de dados, cubos, dimensões, estruturas de mineração e funções.  
  
 Os pré-requisitos incluem a noção de XMLA (XML for Analysis). Felizmente, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem um recurso que cria automaticamente o script XMLA necessário para criar objetos, como cubos. Esse recurso de automação ajuda a reduzir a curva de aprendizagem do XMLA. Para obter mais informações sobre como usar XMLA, consulte [Como desenvolver com XMLA no Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md). Para obter mais informações sobre como usar XMLA, consulte [Como desenvolver com XMLA no Analysis Services](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
> [!IMPORTANT]  
>  Na geração de script de objeto de função, observe que as permissões de segurança estão contidas nos objetos que elas protegem em vez de estarem contidas na função de segurança com as quais elas estão associadas.  
  
#### <a name="to-script-analysis-services-objects"></a>Para gerar scripts de objetos do Analysis Services  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
2.  Localize o objeto para o qual você deseja criar um script que cria, altera ou exclui objetos.  
  
3.  Clique com o botão direito do mouse no objeto, aponte para **Script de Cubo como**, aponte para **CRIAR para**, **ALTERAR para**ou **Excluir para**e, então, clique em uma destas opções: **Nova Janela do Editor de Consulta** para abrir a janela do editor de consultas, **Arquivo** para salvar o script do XMLA em um arquivo ou **Área de Transferência** para salvar o script do XMLA nessa área.  
  
    > [!NOTE]  
    >  Normalmente, você selecionaria **Arquivo** se quisesse criar várias versões diferentes do arquivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar script de tarefas administrativas no Analysis Services](../script-administrative-tasks-in-analysis-services.md)   
 [Editor de Consultas XMLA &#40;Analysis Services – Dados Multidimensionais&#41;](../xmla-query-editor-analysis-services-multidimensional-data.md)  
  
  
