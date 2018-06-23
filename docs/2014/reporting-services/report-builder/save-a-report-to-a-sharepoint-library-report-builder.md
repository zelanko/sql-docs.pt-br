---
title: Salvar um relatório em uma biblioteca do SharePoint (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 9a123b41b39ca2fd4ea4f0e20d1b5ec6678dc5fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118594"
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>Salvar um relatório em uma biblioteca do SharePoint (Construtor de Relatórios)
  Para salvar um relatório em um servidor de relatório configurado para integração com o SharePoint, vá até o servidor do SharePoint e estabeleça uma conexão com o servidor de relatório. Na definição de relatório, todas as referências a itens relacionados ao relatório devem usar valores específicos a um servidor de relatório do SharePoint. Os itens relacionados incluem sub-relatórios, relatórios detalhados e recursos, como imagens baseadas na Web. Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint para definir as propriedades no projeto.  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>Para salvar um relatório em um site do SharePoint  
  
1.  No botão Construtor de Relatórios, clique em **Salvar**. A caixa de diálogo **Salvar como***\<Item de relatório>* é exibida.  
  
    > [!NOTE]  
    >  Se você estiver salvando um relatório de novo, ele será salvo novamente automaticamente em seu local anterior. Use a opção **Salvar como** para alterar o local.  
  
2.  Se desejar, clique em **Sites e Servidores Recentes** para mostrar uma lista de servidores de relatório e sites do SharePoint usados recentemente.  
  
3.  Navegue até o site do SharePoint e clique em **Salvar**.  
  
    > [!NOTE]  
    >  Se você deixar um relatório alterado durante mais de 10 horas sem salvá-lo, ele será desconectado do servidor sem ser salvado. Se isso acontecer, na barra de status inferior direita, clique em **Desconectar**e clique em **Conectar**. O servidor mais recente estará na lista de servidores disponíveis. Selecione-o e o relatório reconectará.  
  
## <a name="see-also"></a>Consulte também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  