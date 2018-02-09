---
title: "Fazer referência às bibliotecas do ADO em um aplicativo Visual Basic 6 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: "“drivers”"
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 937934fd297c876fa023ddae89ac027068bb20c9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Fazer referência às bibliotecas do ADO em um aplicativo Visual Basic 6
Para importar as bibliotecas do ADO para um aplicativo do Microsoft Visual Basic 6, você deve definir uma referência no projeto do Visual Basic.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Para definir uma referência às bibliotecas ADO em um projeto do Visual Basic  
  
1.  Criar um novo ou abrir um projeto existente do Visual Basic.  
  
2.  Clique o **projeto** item de menu e selecione **referências...**  do painel do menu suspenso.  
  
3.  De **referências disponíveis**, marque a caixa de **Microsoft ActiveX Data Objects *n.n* biblioteca**, onde ***n.n*** representa a versão mais recente número de versão. O **local** abaixo do campo deve identificar sua escolha como *$installDir\msado15.dll*, onde *$installDir* representa o caminho do diretório no qual a biblioteca do ADO foi instalado.  
  
4.  Se você pretende usar o ADO MD, repita a etapa 3 para selecionar **Microsoft ActiveX Data Objects (multidimensional) *n.n* biblioteca**. O **local** campo deve identificar essa opção como *$installDir\msadomd.dll*.  
  
5.  Se você pretende usar ADOX, repita a etapa 3 para selecionar **Microsoft ADO Ext. *n.n* DDL e a segurança de**. O **local** campo deve identificar essa opção como *$installDir\msadox.dll*.  
  
6.  Clique em **Okey** para terminar de definir as referências.  
  
## <a name="backward-compatibility"></a>Compatibilidade com versões anteriores  
 Instalar o ADO também copia as seguintes bibliotecas de tipo de versões anteriores:  
  
-   *msado27.tlb*, biblioteca de tipos 2.7 de ADO  
  
-   *msado26.tlb*, ADO 2.6 do tipo biblioteca  
  
-   *msado25.tlb*, biblioteca de tipos de 2,5 de ADO  
  
-   *msado21.tlb*, biblioteca de tipos 2.1 de ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 de ADO  
  
 Se seu aplicativo deve usar uma dessas bibliotecas ADO para fins de compatibilidade com versões anteriores, você precisa importar a versão apropriada da biblioteca de tipos. Para fazer isso, siga os procedimentos na seção anterior, substituindo *msado15.dll* por *msadoXX.tlb*, onde *XX* representa o número de versão, você precisa importar.
