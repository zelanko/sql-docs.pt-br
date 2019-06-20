---
title: Combinar dados (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 67bdfd9b3a8377b05448b73bd41addd4796a9538
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478991"
---
# <a name="combine-data-mds-add-in-for-excel"></a>Combinar dados (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], combine dados de duas planilhas quando você desejar comparar dados antes de publicar. Nesse procedimento, você combina dados de duas planilhas em uma. Assim, você pode executar mais comparações e determinar quais dados, se houver, publicar no repositório do MDS.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve ter uma planilha que contenha dados gerenciados no MDS. Para obter mais informações, consulte [carregar dados do MDS no Excel](export-data-to-excel-from-master-data-services.md).  
  
-   Você deve ter uma planilha que contenha dados que queira combinar com os dados gerenciados no MDS. Essa planilha deve ter uma linha de cabeçalho.  
  
### <a name="to-combine-non-managed-data-into-an-mds-managed-sheet"></a>Para combinar dados não gerenciados em uma planilha gerenciada no MDS  
  
1.  Na planilha que contém dados gerenciados no MDS, no grupo **Publicar e Validar** , clique em **Combinar Dados**.  
  
2.  Na caixa de diálogo **Combinar Dados** , ao lado da caixa de texto **Intervalo a ser combinado com dados do MDS** , clique no ícone. A caixa de diálogo é recolhida.  
  
3.  Clique na planilha que contém os dados que você deseja combinar.  
  
4.  Realce todas as células na planilha que você deseja combinar, inclusive a linha de cabeçalho.  
  
5.  Na caixa de diálogo **Combinar Dados** , clique no ícone. A caixa de diálogo é expandida.  
  
6.  Para uma coluna listada para a entidade do MDS, selecione uma coluna em **Coluna Correspondente**. Nem todas as colunas do MDS precisam de colunas correspondentes.  
  
7.  Clique em **Combinar**. Uma coluna de **SOURCE** é exibida, indicando se os dados são do MDS ou de uma origem externa.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Para localizar semelhanças entre os dados gerenciados no MDS e dados externos, consulte [Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](match-similar-data-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Carregamento de dados &#40;suplemento do MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Correspondência de qualidade de dados no Suplemento do MDS para Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  
