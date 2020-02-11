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
ms.openlocfilehash: 25ea858995c884af202d3d80f4de675c9f4cda27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923058"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Referenciar as bibliotecas ADO em um aplicativo do Visual Basic 6
Para importar as bibliotecas do ADO para um aplicativo do Microsoft Visual Basic 6, você deve definir uma referência no projeto Visual Basic.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Para definir uma referência às bibliotecas ADO em um projeto Visual Basic  
  
1.  Crie um novo projeto do Visual Basic ou abra um existente.  
  
2.  Clique no item de menu **projeto** e, em seguida, selecione **referências...** no painel de menu suspenso.  
  
3.  Em **referências disponíveis**, marque a caixa da **biblioteca Microsoft ActiveX Data Objects *n. n* **, em que ***n. n*** representa o número de versão mais recente. O campo **local** abaixo deve identificar sua escolha como *$installDir \msado15.dll*, em que *$installDir* representa o caminho do diretório no qual a biblioteca ADO foi instalada.  
  
4.  Se você pretende usar ADO MD, repita a etapa 3 para selecionar a **biblioteca do Microsoft ActiveX Data Objects (Multidimensional) *n. n* **. O campo **local** deve identificar essa opção como *$installDir \msadomd.dll*.  
  
5.  Se você pretende usar o ADOX, repita a etapa 3 para selecionar **Microsoft ADO ext. n *. n* para DDL e segurança**. O campo **local** deve identificar essa opção como *$installDir \msadox.dll*.  
  
6.  Clique em **OK** para concluir a configuração das referências.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 A instalação do ADO também copia as seguintes bibliotecas de tipos de versões anteriores:  
  
-   *msado27. tlb*, biblioteca de tipos ADO 2,7  
  
-   *msado26. tlb*, biblioteca de tipos ADO 2,6  
  
-   *msado25. tlb*, biblioteca de tipos ADO 2,5  
  
-   *msado21. tlb*, biblioteca de tipos ADO 2,1  
  
-   *msado20. tlb*, biblioteca de tipos ADO 2,0  
  
 Se seu aplicativo precisar usar qualquer uma dessas bibliotecas ADO por motivos de compatibilidade com versões anteriores, você precisará importar a versão apropriada da biblioteca de tipos. Para fazer isso, siga os procedimentos na seção anterior, substituindo *MsADO15. dll* por *msadoXX. tlb*, em que *XX* representa o número de versão que você precisa importar.
