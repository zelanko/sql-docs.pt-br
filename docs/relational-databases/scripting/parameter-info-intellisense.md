---
title: "Informações sobre parâmetros (IntelliSense) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b76a63705473437b283e104414f3729166ce2338
ms.lasthandoff: 04/11/2017

---
# <a name="parameter-info-intellisense"></a>Informações sobre Parâmetros (IntelliSense)
  A opção [!INCLUDE[msCoName](../../includes/msconame-md.md)] Informações sobre Parâmetros **do** IntelliSense abre uma lista de parâmetros com informações sobre número, nomes e tipos dos parâmetros necessários para uma função ou um procedimento armazenado. O parâmetro em negrito indica o próximo parâmetro exigido à medida que você digita uma função ou um procedimento armazenado.  
  
 A lista de parâmetros também é exibida para funções aninhadas. Se você digitar uma função como um parâmetro para outra função, a lista de parâmetros exibirá os parâmetros da função interna. Em seguida, quando a lista de parâmetros da função interna estiver completa, a lista de parâmetros é revertida para exibir os parâmetros da função externa.  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>Para exibir Informações sobre Parâmetros para funções ou procedimentos armazenados  
  
1.  Depois do nome de uma função, digite um parêntese de abertura como normalmente o faz para abrir a lista de parâmetros. Após digitar o nome de um procedimento armazenado, digite um espaço como normalmente o faz para obter informações sobre os parâmetros do procedimento.  
  
     O IntelliSense exibe a declaração completa da função ou os parâmetros de um procedimento armazenado em uma janela pop-up sob o ponto de inserção. O primeiro parâmetro da lista aparece em negrito.  
  
2.  À medida que você digita os parâmetros, a fonte em negrito se altera para refletir o próximo parâmetro que você precisa digitar.  
  
3.  Pressione ESC a qualquer momento para fechar a lista ou continue digitando até concluir a função.  
  
     Para uma função, se você digitar o parêntese de fechamento, também fechará a lista de parâmetros.  
  
#### <a name="to-manually-start-parameter-info"></a>Para iniciar manualmente as Informações sobre Parâmetros  
  
1.  No menu **Editar** , selecione **IntelliSense** e selecione **Informações sobre Parâmetros**.  
  
2.  Pressione as teclas de atalho CTRL+SHIFT+ESPAÇO.  
  
 Para obter mais informações, consulte [Configurar IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md).  
  
> [!NOTE]  
>  A opção **Informações sobre Parâmetros** só está disponível para o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o Editor de Consultas XML.  
  
  
