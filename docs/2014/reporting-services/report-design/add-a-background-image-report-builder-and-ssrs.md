---
title: Adicionar uma imagem de tela de fundo (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df5de06ef60cf22a023589efb9d67f0f521f1c40
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59942702"
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>Adicionar uma imagem de plano de fundo (Construtor de Relatórios e SSRS)
  Você pode adicionar uma imagem de plano de fundo a um item de relatório tais como um retângulo, uma caixa de texto, uma lista, uma matriz, uma tabela, algumas partes de um gráfico, ou uma seção de relatório como cabeçalho de página, rodapé de página ou corpo de relatório. Você pode definir uma imagem de tela de fundo para qualquer item selecionado na superfície de design do relatório que exiba **BackgroundImage** no painel Propriedades. Assim como outras imagens, a imagem de plano de fundo pode ser uma URL para uma imagem no servidor de relatório, uma imagem de um campo de conjunto de dados ou uma imagem inserida na definição de relatório. Para usar uma imagem inserida no relatório, primeiro adicione a imagem à definição de relatório antes de adicioná-la à superfície de design.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>Para inserir uma imagem na definição de relatório  
  
1.  No painel de dados do relatório, clique com o botão direito do mouse no nó **Imagens** e clique em **Adicionar Imagem**.  
  
    > [!NOTE]  
    >  Se o painel de dados do relatório não estiver visível, clique em **Dados do Relatório** na guia **Exibir**.  
  
2.  Navegue até a imagem a ser inserida em sua definição de relatório e clique em **OK**.  
  
### <a name="to-add-a-background-image"></a>Para adicionar uma imagem de plano de fundo  
  
1.  No modo Design de Relatório, selecione o item de relatório ao qual você deseja adicionar uma imagem de plano de fundo.  
  
2.  Se o painel Propriedades não estiver visível, na guia **Exibir** , selecione **Propriedades**.  
  
3.  No painel Propriedades, expanda **BackgroundImage**e faça o seguinte:  
  
    -   Para uma imagem inserida:  
  
         Defina **Origem** como **Inserida**.  
  
         Defina **Valor** como o nome de uma imagem que é inserida no relatório.  
  
    -   Para uma imagem externa:  
  
         Defina **Origem** como **Externa**.  
  
         Defina **Valor** como um caminho válido para uma imagem. Ele pode estar em um servidor de relatório em modo nativo ou em modo Integrado do SharePoint, ou ele pode estar em qualquer outro site. Para obter mais informações, consulte [Adicionar uma imagem externa &#40;Construtor de Relatórios e SSRS&#41;](add-an-external-image-report-builder-and-ssrs.md).  
  
    -   Para uma imagem contida em um campo do banco de dados ao qual o item de relatório está conectado:  
  
         Defina **Origem** como **Banco de Dados**.  
  
         Defina **Valor** como o nome de um campo no conjunto de dados de relatório. Para obter mais informações, consulte [Adicionar uma imagem com limite de dados &#40;Construtor de Relatórios e SSRS&#41;](add-a-data-bound-image-report-builder-and-ssrs.md).  
  
         Para **MIMEType** ou formato de arquivo, selecione o tipo MIME adequado para a imagem; por exemplo, .bmp.  
  
        > [!NOTE]  
        >  MIMEType só poderá ser aplicado se a propriedade **Source** estiver definida como **Banco de Dados**. Se a propriedade **Source** estiver definida como **Externa** ou **Inserida**, o valor **MIMEType** será ignorado.  
  
    -   Para **BackgroundRepeat**, selecione uma expressão, **Default**, **Repeat**, **RepeatX**ou **RepeatY**ou **Clip**.  
  
         Para as imagens de tela de fundo em um gráfico, **BackgroundRepeat** poderá ser definido como **Default**, **Repeat**, **Fit**e **Clip**, mas não **RepeatX** ou **RepeatY**.  
  
## <a name="see-also"></a>Consulte também  
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](images-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
