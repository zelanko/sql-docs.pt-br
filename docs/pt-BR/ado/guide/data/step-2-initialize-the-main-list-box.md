---
title: 'Etapa 2: Inicializar a caixa de listagem principal | Microsoft Docs'
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afef142bef13daea6ba03fa967f87198c6ebe662
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="step-2-initialize-the-main-list-box"></a>Etapa 2: Inicializar a caixa de listagem principal
Para declarar objetos globais de registro e o conjunto de registros, insira o código a seguir (geral) (declarações) para Form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Esse código declara as referências de objeto global para objetos de registro e o conjunto de registros que serão usadas posteriormente nesse cenário.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Para se conectar a uma URL e popular lstMain  
 Insira o seguinte código para o manipulador de eventos de carregar formulário para Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=http://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Esse código cria uma instância de objetos globais de registro e o conjunto de registros. O objeto de registro, `grec`, é aberta com uma URL especificada como o ActiveConnection. Se a URL existir, ele é aberto; Se ele ainda não existir, ele será criado. Observe que você deve substituir "http://servername/foldername/" com uma URL válida de seu ambiente.  
  
 O objeto de conjunto de registros, `grs`, é aberta nos filhos do registro, `grec`. Em seguida, `lstMain` é preenchida com os nomes de arquivo dos recursos publicados para a URL.  
  
## <a name="see-also"></a>Consulte também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 1: Configurar o projeto do Visual Basic](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Etapa 3: Preencher a caixa de listagem de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
