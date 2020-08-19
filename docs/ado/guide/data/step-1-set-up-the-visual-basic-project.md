---
description: 'Etapa 1: Configurar o projeto do Visual Basic'
title: 'Etapa 1: configurar o projeto de Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: rothja
ms.author: jroth
ms.openlocfilehash: d168a136d4cc80999591f0e36cb65abefa9c6c79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452808"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Etapa 1: Configurar o projeto do Visual Basic
Nesse cenário, supõe-se que você tenha o Microsoft Visual Basic 6,0, ADO 2,5 ou posterior e o provedor de OLE DB da Microsoft para publicação na Internet instalado no seu sistema. Primeiro, você criará um novo projeto e, em seguida, adicionará alguns controles ao formulário padrão no projeto.  
  
### <a name="to-create-an-ado-project"></a>Para criar um projeto ADO:  
  
1.  No Microsoft Visual Basic, crie um novo projeto Standard EXE.  
  
2.  No menu projeto, escolha referências.  
  
3.  Selecione "biblioteca do Microsoft ActiveX Data Objects 2,5" e clique em OK.  
  
### <a name="to-insert-controls-on-the-main-form"></a>Para inserir controles no formulário principal:  
  
1.  Adicione um controle ListBox ao Form1. Defina sua propriedade Name como **lstMain**.  
  
2.  Adicione outro controle ListBox ao Form1. Defina sua propriedade Name como **lstDetails**.  
  
3.  Adicione um controle TextBox ao Form1. Defina sua propriedade Name como **txtDetails**.  
  
## <a name="see-also"></a>Consulte Também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 2: Inicializar a caixa de listagem principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
