---
title: Propriedades do servidor (página Histórico) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
caps.latest.revision: 28
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: b8e5a906afeb39effa9dc72601748f45c70be6bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013272"
---
# <a name="server-properties-history-page"></a>Propriedades do Servidor (página Histórico)
  Use essa página para definir um valor padrão para o número de cópias do histórico de relatório a serem retidas. O valor padrão fornece uma configuração inicial que estabelece limites de histórico de relatório para todos os relatórios. Você pode variar essas configurações para relatórios individuais.  
  
 Histórico de relatório é uma coleção de instantâneos de relatórios que inclui dados do relatório e o layout atual do relatório no momento em que o instantâneo foi criado. Você pode usar o histórico de relatórios para manter uma cópia de um relatório como ele era em uma data e hora específica. Você pode criar e gerenciar histórico de relatório para relatórios individuais executados em um servidor de relatório no modo nativo ou um servidor de relatório configurado para o modo integrado do SharePoint.  
  
 Instantâneos de relatórios são armazenados no banco de dados do servidor de relatório. Se você mantém um número ilimitado de instantâneos, verifique periodicamente o tamanho do banco de dados para se certificar de que ele não esteja crescendo com muita rapidez ou consumindo muito espaço em disco.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância de servidor de relatórios, clique com o botão direito do mouse no nome do servidor de relatórios e selecione **Propriedades**. Clique em **Histórico** para abrir essa página.  
  
## <a name="options"></a>Opções  
 **Manter um número ilimitado de instantâneos no histórico de relatório**  
 Retenha todos os instantâneos de histórico de relatório. Você deve excluir instantâneos manualmente para reduzir o tamanho de histórico de relatórios.  
  
 **Limitar as cópias do histórico de relatório**  
 Retenha um número de conjunto de instantâneos de histórico de relatório. Quando o limite é alcançado, cópias mais antigas são removidas do histórico do relatório para liberar espaço para cópias mais atuais.  
  
 Se, posteriormente, você limitar o histórico de relatório, quando o histórico existente exceder o limite especificado, o servidor de relatório reduzirá o histórico existente ao novo limite. Os instantâneos de relatórios mais antigos são excluídos primeiro. Se o histórico de relatórios estiver vazio ou abaixo do limite, novos instantâneos de relatório serão adicionados. Quando o limite é alcançado, o instantâneo mais antigo é excluído e um novo instantâneo de relatório é adicionado.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)  
  
  