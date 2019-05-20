---
title: Desenvolver uma interface do usuário para um enumerador ForEach personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d72d8fba0d9fbe68b14ebc06cbb8d171ef08ddd3
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724552"
---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>Desenvolvendo uma interface do usuário para um enumerador ForEach personalizado

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Depois de ter substituído a implementação das propriedades e dos métodos da classe base para ter sua funcionalidade personalizada, convém que você crie uma interface de usuário personalizada para o enumerador Foreach. Se você não criar uma interface de usuário personalizada, os usuários só poderão configurar o novo enumerador Foreach personalizado usando a janela Propriedades.  
  
 Em um projeto ou assembly de interface de usuário personalizada, você cria uma classe que implementa <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>. Essa classe deriva de System.Windows.Forms.UserControl, que normalmente é usado para criar um controle de composição para hospedar outros controles do Windows Forms. O controle que você cria é exibido na área **Configuração do enumerador** da guia **Coleção** do **Editor de Loop Foreach**.  
  
> [!IMPORTANT]  
>  Depois de assinar e criar sua interface do usuário personalizada e instalá-la no cache de assembly global, conforme descrito em [Compilar, implantar e depurar objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md), lembre-se de fornecer o nome totalmente qualificado desta classe na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>.  
  
## <a name="coding-the-user-interface-control-class"></a>Codificando a classe de controle de interface do usuário  
  
### <a name="initializing-the-user-interface"></a>Inicializando a interface do usuário   
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> para referências de cache ao objeto de host e às coleções de gerenciadores de conexões e variáveis definidas no pacote.  
  
### <a name="setting-properties-on-the-user-interface-control"></a>Definindo propriedades no controle de interface do usuário  
 A classe UserControl, cuja classe de interface do usuário é derivada, destina-se a ser utilizada como um controle de composição para hospedar outros controles do Windows Forms. Como essa classe hospeda outros controles, você poderá criar sua interface de usuário personalizada arrastando e soltando os controles, organizando-os, definindo suas propriedades e respondendo em tempo de execução a seus eventos como em qualquer aplicativo do Windows Forms.  
  
### <a name="saving-settings"></a>Salvando configurações  
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> para copiar os valores selecionados pelo usuário dos controles para as propriedades do enumerador quando o usuário fecha o editor.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [Codificar um enumerador Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  
