---
description: 'Etapa 2: Inicializar a caixa de listagem principal'
title: 'Etapa 2: inicializar a caixa de listagem principal | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: rothja
ms.author: jroth
ms.openlocfilehash: f746b454b18de7d88ca4c42d049eb058f671ba8e
ms.sourcegitcommit: 291ae8f6b72fd355f8f24ce5300339306293ea7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512292"
---
# <a name="step-2-initialize-the-main-list-box"></a>Etapa 2: Inicializar a caixa de listagem principal
Para declarar os objetos de registro global e conjunto de registros, insira o seguinte código no (geral) (declarações) para Form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Esse código declara referências de objeto global para objetos de registro e conjunto de registros que serão usados posteriormente neste cenário.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Para se conectar a uma URL e popular lstMain  
 Insira o seguinte código no manipulador de eventos de carregamento de formulário para Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Esse código instancia os objetos de registro global e conjunto de registros. O objeto Record, `grec` , é aberto com uma URL especificada como a ActiveConnection. Se a URL existir, ela será aberta; Se ele ainda não existir, ele será criado. Observe que você deve substituir `https://servername/foldername/` por uma URL válida do seu ambiente.  
  
 O objeto recordset, `grs` , é aberto nos filhos do registro, `grec` . Em seguida, `lstMain` é populado com os nomes de arquivo dos recursos publicados na URL.  
  
## <a name="see-also"></a>Consulte Também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 1: configurar o projeto de Visual Basic](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Etapa 3: Preencher a caixa de listagem de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
