---
title: Adicionar HTML a um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 147daad87bf9ec77d2c686d44d367e85a07ab4c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63021295"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>Adicionar um HTML a um relatório (Construtor de Relatórios e SSRS)
  Usando um espaço reservado, você pode importar HTML de um campo em seu conjunto de dados para usar no relatório. Por padrão, um espaço reservado representa texto sem-formatação, portanto você precisará alterar o tipo de marcação do espaço reservado para HTML. Para obter mais informações, consulte [Importando HTML para um relatório &#40;Construtor de Relatórios e SSRS&#41;](importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>Para adicionar HTML de um campo em seu conjunto de dados a uma caixa de texto  
  
1.  Na guia **Inserir** , clique em **Lista**. Clique na superfície de design e arraste-a para criar uma caixa com o tamanho desejado.  
  
     A caixa de diálogo **Propriedades do Conjunto de Dados** é aberta. Você pode usar um conjunto de dados compartilhado ou um conjunto de dados inserido em seu relatório. Para obter mais informações, clique em [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta &#40;Construtor de Relatórios&#41;](../report-data/dataset-properties-dialog-box-query-report-builder.md) ou [Caixa de diálogo Propriedades do Conjunto de Dados, Consulta](../dataset-properties-dialog-box-query.md).  
  
2.  Na guia **Inserir** , clique em **Caixa de Texto**. Clique na lista e arraste-a para criar uma caixa com o tamanho desejado.  
  
3.  Arraste um campo HTML do conjunto de dados para a caixa de texto. Será criado um espaço reservado para seu campo.  
  
4.  Clique com o botão direito do mouse no espaço reservado e depois em **Propriedades do Espaço Reservado**.  
  
5.  Na guia **Geral** , verifique se a caixa **Valor** contém uma expressão que avalie para o campo descartado na etapa 3.  
  
6.  Clique em **HTML – Interpretar marcas HTML como estilos**. Isso faz com que o campo seja avaliado como HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](images-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades do Espaço Reservado, Geral &#40;Construtor de Relatórios e SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
