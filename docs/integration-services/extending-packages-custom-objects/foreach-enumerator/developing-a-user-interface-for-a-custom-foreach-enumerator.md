---
title: "Desenvolvendo uma Interface de usuário para um enumerador ForEach personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e743464fcf482ea51f0cde78d692b367c2be525b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>Desenvolvendo uma interface do usuário para um enumerador ForEach personalizado
  Depois de ter substituído a implementação das propriedades e dos métodos da classe base para ter sua funcionalidade personalizada, convém que você crie uma interface de usuário personalizada para o enumerador Foreach. Se você não criar uma interface de usuário personalizada, os usuários só poderão configurar o novo enumerador Foreach personalizado usando a janela Propriedades.  
  
 Em um projeto ou assembly de interface de usuário personalizada, você cria uma classe que implementa <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>. Essa classe deriva de UserControl, que normalmente é usado para criar um controle composto para hospedar outros controles de formulários do Windows. O controle que você cria é exibido no **configuração do enumerador** área do **coleção** guia do **Editor de Loop Foreach**.  
  
> [!IMPORTANT]  
>  Depois de assinar e criar sua interface de usuário personalizada e instalá-la no cache de assembly global, conforme descrito em [compilando, implantando e depurando objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md), lembre-se de fornecer o nome totalmente qualificado desta classe no <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> propriedade o <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
## <a name="coding-the-user-interface-control-class"></a>Codificando a classe de controle de interface do usuário  
  
### <a name="initializing-the-user-interface"></a>Inicializando a interface do usuário   
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> para referências de cache ao objeto de host e às coleções de gerenciadores de conexões e variáveis definidas no pacote.  
  
### <a name="setting-properties-on-the-user-interface-control"></a>Definindo propriedades no controle de interface do usuário  
 Classe UserControl, da qual a classe de interface do usuário é derivada, destina-se ao uso como um controle composto para hospedar outros controles de formulários do Windows. Como essa classe hospeda outros controles, você poderá criar sua interface de usuário personalizada arrastando e soltando os controles, organizando-os, definindo suas propriedades e respondendo em tempo de execução a seus eventos como em qualquer aplicativo do Windows Forms.  
  
### <a name="saving-settings"></a>Salvando configurações  
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> para copiar os valores selecionados pelo usuário dos controles para as propriedades do enumerador quando o usuário fecha o editor.  
  
## <a name="see-also"></a>Consulte também  
 [Criação de um enumerador de Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [Codificando um enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  
