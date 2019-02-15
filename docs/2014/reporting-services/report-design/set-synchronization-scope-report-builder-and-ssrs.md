---
title: Definir o escopo da sincronização (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3c2286ec6a8995d6fe707690629cbcce0dede127
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293384"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>Definir o escopo da sincronização (Construtor de Relatórios e SSRS)
  Os indicadores transmitem valores de dados fazendo a sincronização do intervalo de valores de dados de indicador em um escopo especificado. Por padrão, o escopo é o contêiner pai do indicador, como a tabela ou matriz que contém o indicador. Você pode alterar a sincronização do indicador dependendo do layout do seu relatório. Por exemplo, se uma região de dados, como uma tabela, tiver um grupo de linhas, você poderá especificar o grupo como o escopo de indicador. O indicador também pode omitir a sincronização.  
  
 Opções como unidades de medida podem ser definidas usando expressões. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
 Para obter informações gerais sobre como entender e definir escopo em relatórios, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-synchronization-scope-of-an-indicator"></a>Para alterar o escopo da sincronização de um indicador  
  
1.  Clique com o botão direito do mouse no indicador que você deseja alterar e clique em **Propriedades do Indicador**.  
  
2.  Clique em **Valores e Estados** no painel esquerdo.  
  
3.  Na lista **Escopo da sincronização** , clique no escopo que você deseja aplicar.  
  
     A opção **(Nenhum)** , que remove o escopo da sincronização do indicador, está sempre disponível. Outras opções dependem do layout do relatório.  
  
     Se desejar, clique no botão **Expressão** (*fx*) para editar uma expressão que define o escopo.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
