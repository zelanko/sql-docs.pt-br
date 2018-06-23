---
title: 'Tarefa 6: Definindo sinônimos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3019c7cf3466fae5579548e3aa8fa9c028145f98
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008521"
---
# <a name="task-6-setting-synonyms"></a>Tarefa 6: Definindo sinônimos
  Nesta tarefa, você define dois valores de domínio, **USA** e **United States**, do domínio **Country** como sinônimos, sendo **United States** o valor principal. Como a opção **Usar Valores Principais** foi selecionada durante a criação do domínio **Country** , todos os valores **USA** do domínio **Country** serão gerados como **United States** (porque United States é o valor principal). Consulte [Alterar Valores de Domínio](http://msdn.microsoft.com/library/hh510408.aspx) para obter mais detalhes.  
  
1.  Selecione **Country** na lista de domínios.  
  
2.  Alterne para a guia **Valores de Domínio** .  
  
3.  Clique no botão **Adicionar novo valor de domínio** na barra de ferramentas.  
  
4.  Digite **USA** como valor e pressione **ENTER**.  
  
5.  Selecione vários valores **United States** e **USA** usando as teclas CTRL ou SHIFT, clique com o botão direito do mouse nos itens selecionados e clique em **Definir como Sinônimo**. O DQS agrupará esses valores e designará um deles como o valor principal que substituirá os outros.  
  
     ![Menu definir como sinônimos](../../2014/tutorials/media/et-settingsynonyms-01.jpg "Menu definir como sinônimos")  
  
6.  Observe que **United States** está definido como valor principal. Se você quiser que USA seja o valor principal, clique com o botão direito do mouse em USA e selecione a opção **Definir como Principal** . Neste tutorial, usamos **United States** como valor principal.  
  
     ![Estados Unidos e EUA como sinônimos](../../2014/tutorials/media/et-settingsynonyms-02.jpg "dos Estados Unidos e EUA como sinônimos")  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 7: Criando uma domínio composto](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  