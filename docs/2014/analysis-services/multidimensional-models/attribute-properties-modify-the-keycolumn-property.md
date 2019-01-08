---
title: Modificar a propriedade KeyColumn de um atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92624d18c0e8aae6a549f0769277e5fd4fdd0c34
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524357"
---
# <a name="modify-the-keycolumn-property-of-an-attribute"></a>Modificar a propriedade KeyColumn de um atributo
  Você pode modificar a propriedade **KeyColumns** de um atributo. Por exemplo, convém especificar uma chave composta em vez de uma chave única como a chave para o atributo.  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>Para modificar a propriedade KeyColumn de um atributo  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto no qual você quer modificar a propriedade **KeyColumns** .  
  
2.  Abra o Designer de Dimensão seguindo um destes procedimentos:  
  
    -   No **Gerenciador de Soluções**, clique com o botão direito do mouse na dimensão na pasta **Dimensões** e, em seguida, clique em **Abrir** ou **Designer de Exibição**.  
  
         -ou-  
  
    -   No Designer de cubo, sobre o **estrutura do cubo** guia, expanda a dimensão do cubo na **dimensões** painel e clique em **editar \<dimensão >**.  
  
3.  Na guia **Estrutura da Dimensão** , no painel **Atributos** , clique no atributo cuja propriedade **KeyColumns** você quer modificar.  
  
4.  Na janela **Propriedades** , clique o valor da propriedade **KeyColumns** .  
  
5.  Clique no botão Procurar **(...)** que aparece na célula de valor da caixa de propriedade.  
  
     A caixa de diálogo **Colunas de Chave** é aberta.  
  
6.  Para remover uma coluna de chave existente, na lista **Colunas de Chave** , selecione a coluna e, em seguida, clique no botão **\<** .  
  
7.  Para adicionar uma coluna de chave, na lista **Colunas Disponíveis** , selecione a coluna e clique no botão **>** .  
  
    > [!NOTE]  
    >  Se você definir várias colunas de chave, a ordem de disposição das colunas na lista **Colunas de Chave** vai afetar a ordem de exibição. Por exemplo, um atributo de mês tem duas colunas de chave: mês e ano. Se a coluna de ano aparecer na lista antes da coluna de mês, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fará a classificação por ano e, depois, por mês. Se a coluna de mês aparecer antes da coluna de ano, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fará a classificação por mês e, depois, por ano.  
  
8.  Para alterar a ordem das colunas de chave, selecione uma coluna e clique no botão **Acima** ou **Abaixo** .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)  
  
  
