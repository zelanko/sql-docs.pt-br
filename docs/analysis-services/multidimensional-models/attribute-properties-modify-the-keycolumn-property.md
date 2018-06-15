---
title: Modificar a propriedade KeyColumn de um atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 278780dd8457a90a6ee2fba632216bd1697ec0f7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021483"
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
  
  
