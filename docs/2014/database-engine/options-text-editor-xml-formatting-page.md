---
title: Opções (página Editor de texto – XML – formatação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ba863207c367e15f72e68885c6011ef485f6201
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929615"
---
# <a name="options-text-editor---xml---formatting-page"></a>Opções (página Editor de texto – XML – Formatação)

Esta caixa de diálogo permite que você especifique as configurações de formatação para o Editor de XML. Você pode acessar a caixa de diálogo **Opções** no menu **Ferramentas**.  
  
> [!NOTE]  
> Estas configurações estão disponíveis quando você seleciona a pasta **Editor de Texto**, a pasta **XML** e a opção **Formatação** na caixa de diálogo **Opções**.  
  
## <a name="attributes"></a>Atributos  
 **Preservar formatação manual de atributos**  
 Não reformate os atributos. Este é o padrão.  
  
> [!NOTE]  
>  Se os atributos estiverem em linhas múltiplas, o editor recua cada linha de atributos para corresponder ao recuo do elemento pai.  
  
 **Alinhar cada atributo em uma linha separada**  
 Alinha o segundo e os atributos subsequentes verticalmente para corresponder ao recuo do primeiro atributo. O seguinte texto XML é um exemplo de como os atributos seriam alinhados.  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>Reformatação Automática  
 **Ao colar da área de transferência.**  
 Reformata o texto XML colado da área de transferência.  
  
 **Ao concluir a marca final**  
 Reformata o elemento quando a marca final é concluída.  
  
## <a name="mixed-content"></a>Conteúdo Misto  
 **Formatar conteúdo misto por padrão.**  
 Tenta reformatar conteúdo misto, exceto quando o conteúdo encontra-se em um escopo `xml:space="preserve"`. Este é o padrão.  
  
 Se um elemento contiver uma mistura de texto e marcação, os conteúdos serão considerados de conteúdo misto. A seguir há um exemplo de um elemento com conteúdo misto.  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</dir>  
  
## <a name="see-also"></a>Consulte Também  
 [Editor XML &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)  
