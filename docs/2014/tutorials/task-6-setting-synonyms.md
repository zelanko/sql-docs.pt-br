---
title: 'Tarefa 6: Definindo sinônimos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a81a538e2cd15dd38a6c32993395cac20079b6f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866322"
---
# <a name="task-6-setting-synonyms"></a>Tarefa 6: Definir sinônimos
  Nesta tarefa, você define dois valores de domínio, **USA** e **United States**, do domínio **Country** como sinônimos, sendo **United States** o valor principal. Como a opção **Usar Valores Principais** foi selecionada durante a criação do domínio **Country** , todos os valores **USA** do domínio **Country** serão gerados como **United States** (porque United States é o valor principal). Consulte [Alterar Valores de Domínio](https://msdn.microsoft.com/library/hh510408.aspx) para obter mais detalhes.  
  
1.  Selecione **Country** na lista de domínios.  
  
2.  Alterne para a guia **Valores de Domínio** .  
  
3.  Clique no botão **Adicionar novo valor de domínio** na barra de ferramentas.  
  
4.  Digite **USA** como valor e pressione **ENTER**.  
  
5.  Selecione vários valores **United States** e **USA** usando as teclas CTRL ou SHIFT, clique com o botão direito do mouse nos itens selecionados e clique em **Definir como Sinônimo**. O DQS agrupará esses valores e designará um deles como o valor principal que substituirá os outros.  
  
     ![Menu definir como sinônimos](../../2014/tutorials/media/et-settingsynonyms-01.jpg "Menu definir como sinônimos")  
  
6.  Observe que **United States** está definido como valor principal. Se você quiser que USA seja o valor principal, clique com o botão direito do mouse em USA e selecione a opção **Definir como Principal** . Neste tutorial, usamos **United States** como valor principal.  
  
     ![Estados Unidos e EUA como sinônimos](../../2014/tutorials/media/et-settingsynonyms-02.jpg "dos Estados Unidos e EUA como sinônimos")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 7: Criar um domínio composto](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  
