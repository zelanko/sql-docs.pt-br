---
title: Referenciando as bibliotecas ADO em um aplicativo Visual Basic 6 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8e37459c5e48fe817a3bdbb6a824550cf977f66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696965"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Referenciar as bibliotecas ADO em um aplicativo do Visual Basic 6
Para importar as bibliotecas ADO em um aplicativo do Microsoft Visual Basic 6, você deve definir uma referência no projeto do Visual Basic.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Para definir uma referência para as bibliotecas ADO em um projeto do Visual Basic  
  
1.  Criar um novo ou abrir um projeto existente do Visual Basic.  
  
2.  Clique o **Project** item de menu e selecione **referências...**  do painel do menu suspenso.  
  
3.  Partir **referências disponíveis**, marque a caixa **Microsoft ActiveX Data Objects *n.n* biblioteca**, onde ***n.n*** representa a versão mais recente número de versão. O **local** campo abaixo deve identificar sua escolha, como *$installDir\msado15.dll*, onde *$installDir* representa o caminho do diretório em que a biblioteca do ADO foi instalado.  
  
4.  Se você pretende usar o ADO MD, repita a etapa 3 para selecionar **Microsoft ActiveX Data Objects (multidimensional) *n.n* biblioteca**. O **local** campo deve identificar essa opção como *$installDir\msadomd.dll*.  
  
5.  Se você pretende usar ADOX, repita a etapa 3 para selecionar **Microsoft ADO ramal *n.n* DDL e segurança**. O **local** campo deve identificar essa opção como *$installDir\msadox.dll*.  
  
6.  Clique em **Okey** para terminar de definir as referências.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Instalar o ADO também copia a bibliotecas de tipo de versões anteriores:  
  
-   *msado27.tlb*, biblioteca de tipos de 2,7 do ADO  
  
-   *msado26.tlb*, biblioteca de tipos de 2,6 do ADO  
  
-   *msado25.tlb*, biblioteca de tipos de 2,5 do ADO  
  
-   *msado21.tlb*, biblioteca de tipos 2.1 de ADO  
  
-   *msado20.tlb*, biblioteca de tipos de 2.0 do ADO  
  
 Se seu aplicativo deve usar qualquer uma dessas bibliotecas ADO para fins de compatibilidade com versões anteriores, você precisa importar a versão apropriada da biblioteca de tipos. Para fazer isso, siga os procedimentos na seção anterior, substituindo *msado15.dll* pela *msadoXX.tlb*, onde *XX* representa o número de versão, você precisa importar.
