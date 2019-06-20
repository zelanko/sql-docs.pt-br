---
title: 'Etapa 1: Configurar o projeto do Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b5f6379eb6cfc1d0f9020019d543cda180d9d88b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700605"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Etapa 1: Configurar o projeto do Visual Basic
Nesse cenário, supõe-se que você tenha o Microsoft Visual Basic 6.0, ADO 2.5 ou posterior e o Microsoft OLE DB Provider para publicação na Internet instalado em seu sistema. Você primeiro crie um novo projeto e, em seguida, adicione alguns controles ao formulário padrão no projeto.  
  
### <a name="to-create-an-ado-project"></a>Para criar um projeto do ADO:  
  
1.  No Microsoft Visual Basic, crie um novo projeto Standard EXE.  
  
2.  No menu projeto, escolha as referências.  
  
3.  Selecione "Microsoft ActiveX Data Objects 2.5 Library" e clique em Okey.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Para inserir controles no formulário principal:  
  
1.  Adicione um controle ListBox ao Form1. Defina sua propriedade de nome como **lstMain**.  
  
2.  Adicione outro controle de caixa de listagem para Form1. Defina sua propriedade de nome como **lstDetails**.  
  
3.  Adicione um controle de caixa de texto para Form1. Defina sua propriedade de nome como **txtDetails**.  
  
## <a name="see-also"></a>Consulte também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 2: Inicializar a caixa de listagem principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
