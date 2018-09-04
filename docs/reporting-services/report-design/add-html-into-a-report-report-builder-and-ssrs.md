---
title: Adicionar HTML a um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cfabee1bb1babb70bd21fc028c87fc840fc9678d
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265048"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>Adicionar um HTML a um relatório (Construtor de Relatórios e SSRS)
  Usando um espaço reservado, você pode importar HTML de um campo em seu conjunto de dados para usar no relatório. Por padrão, um espaço reservado representa texto sem-formatação, portanto você precisará alterar o tipo de marcação do espaço reservado para HTML. Para obter mais informações, consulte [Importando HTML para um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>Para adicionar HTML de um campo em seu conjunto de dados a uma caixa de texto  
  
1.  Na guia **Inserir** , clique em **Lista**. Clique na superfície de design e arraste-a para criar uma caixa com o tamanho desejado.  
  
     A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta. Você pode usar um conjunto de dados compartilhado ou um conjunto de dados inserido em seu relatório. Para obter mais informações, clique em [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) ou [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f).  
  
2.  Na guia **Inserir** , clique em **Caixa de Texto**. Clique na lista e arraste-a para criar uma caixa com o tamanho desejado.  
  
3.  Arraste um campo HTML do conjunto de dados para a caixa de texto. Será criado um espaço reservado para seu campo.  
  
4.  Clique com o botão direito do mouse no espaço reservado e depois em **Propriedades do Espaço Reservado**.  
  
5.  Na guia **Geral** , verifique se a caixa **Valor** contém uma expressão que avalie para o campo descartado na etapa 3.  
  
6.  Clique em **HTML – Interpretar marcas HTML como estilos**. Isso faz com que o campo seja avaliado como HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Espaço Reservado, Geral &#40;Construtor de Relatórios e SSRS&#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
