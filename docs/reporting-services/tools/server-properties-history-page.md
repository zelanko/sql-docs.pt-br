---
title: "Propriedades do servidor (página Histórico) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66744654fac383f2390109a01f8d4cb7b502bf7a
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="server-properties-history-page"></a>Propriedades do Servidor (página Histórico)
  Use essa página [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] em [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para definir um valor padrão para o número de cópias do histórico de relatório a serem retidas. O valor padrão fornece uma configuração inicial que estabelece limites de histórico de relatório para todos os relatórios. Você pode variar essas configurações para relatórios individuais.  
  
 Histórico de relatório é uma coleção de instantâneos de relatórios que inclui dados do relatório e o layout atual do relatório no momento em que o instantâneo foi criado. Você pode usar o histórico de relatórios para manter uma cópia de um relatório como ele era em uma data e hora específica. Você pode criar e gerenciar histórico de relatório para relatórios individuais executados em um servidor de relatório no modo nativo ou um servidor de relatório configurado para o modo integrado do SharePoint.  
  
 Instantâneos de relatórios são armazenados no banco de dados do servidor de relatório. Se você mantém um número ilimitado de instantâneos, verifique periodicamente o tamanho do banco de dados para se certificar de que ele não esteja crescendo com muita rapidez ou consumindo muito espaço em disco.  
  
 Para abrir esta página:
 1) Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Conecte-se a uma instância do servidor de relatório.
 3) Clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**.
 4) Clique em **Histórico** para abrir essa página.  
  
## <a name="options"></a>Opções  
 **Manter um número ilimitado de instantâneos no histórico de relatório**  
 Retenha todos os instantâneos de histórico de relatório. Você deve excluir instantâneos manualmente para reduzir o tamanho de histórico de relatórios.  
  
 **Limitar as cópias do histórico de relatório**  
 Retenha um número de conjunto de instantâneos de histórico de relatório. Quando o limite é alcançado, cópias mais antigas são removidas do histórico do relatório para liberar espaço para cópias mais atuais.  
  
 Se, posteriormente, você limitar o histórico de relatório, quando o histórico existente exceder o limite especificado, o servidor de relatório reduzirá o histórico existente ao novo limite. Os instantâneos de relatórios mais antigos são excluídos primeiro. Se o histórico de relatórios estiver vazio ou abaixo do limite, novos instantâneos de relatório serão adicionados. Quando o limite é alcançado, o instantâneo mais antigo é excluído e um novo instantâneo de relatório é adicionado.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  

