---
title: Modificar a propriedade KeyColumn de um atributo | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e745159dbb8a8e329ad5cbdee64831ce284439c8
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="attribute-properties---modify-the-keycolumn-property"></a>Propriedades de atributo - modificar a propriedade KeyColumn
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Você pode modificar a propriedade **KeyColumns** de um atributo. Por exemplo, convém especificar uma chave composta em vez de uma chave única como a chave para o atributo.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>Para modificar a propriedade KeyColumn de um atributo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto no qual você quer modificar a propriedade **KeyColumns** .  
  
2.  Abra o Designer de Dimensão seguindo um destes procedimentos:  
  
    -   No **Gerenciador de Soluções**, clique com o botão direito do mouse na dimensão na pasta **Dimensões** e, em seguida, clique em **Abrir** ou **Designer de Exibição**.  
  
         — ou —  
  
    -   No Designer de cubo no **estrutura do cubo** guia, expanda a dimensão do cubo no **dimensões** painel e clique em **editar \<dimensão >**.  
  
3.  Na guia **Estrutura da Dimensão**, no painel **Atributos**, clique no atributo cuja propriedade **KeyColumns** você quer modificar.  
  
4.  Na janela **Propriedades** , clique o valor da propriedade **KeyColumns** .  
  
5.  Clique no botão Procurar **(...)** que aparece na célula de valor da caixa de propriedade.  
  
     A caixa de diálogo **Colunas de Chave** é aberta.  
  
6.  Para remover uma coluna de chave existente, na lista **Colunas de Chave** , selecione a coluna e, em seguida, clique no botão **\<** .  
  
7.  Para adicionar uma coluna de chave, na lista **Colunas Disponíveis** , selecione a coluna e clique no botão **>** .  
  
    > [!NOTE]  
    >  Se você definir várias colunas de chave, a ordem de disposição das colunas na lista **Colunas de Chave** vai afetar a ordem de exibição. Por exemplo, um atributo de mês tem duas colunas de chave: mês e ano. Se a coluna de ano aparecer na lista antes da coluna de mês, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fará a classificação por ano e, depois, por mês. Se a coluna de mês aparecer antes da coluna de ano, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fará a classificação por mês e, depois, por ano.  
  
8.  Para alterar a ordem das colunas de chave, selecione uma coluna e clique no botão **Acima** ou **Abaixo** .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
