---
title: Excluir itens de catálogo (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.deleteitems.f1
ms.assetid: b0599e01-6dc3-4484-80d4-022a412e0ebd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c951e24c2d16de2fb3d5fbb6ba63fee8f143bcfd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217830"
---
# <a name="delete-catalog-items-management-studio"></a>Excluir itens do catálogo (Management Studio)
  Use essa página para excluir agendas compartilhadas e definições de função.  
  
 Se uma agenda compartilhada usada por vários relatórios e assinaturas for excluída, o servidor de relatório criará agendas individuais para cada relatório e assinatura que usou anteriormente a agenda compartilhada. Cada nova agenda individual conterá a data, a hora e o padrão de recorrência que foram especificados na agenda compartilhada. Observe que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece o gerenciamento central de agendas individuais. Se você excluir uma agenda compartilhada, deverá manter as informações de agenda para cada item individual. Antes de excluir uma agenda compartilhada, use a [página Relatórios](schedule-properties-reports-page.md) para determinar quais relatórios estão usando a agenda compartilhada atualmente.  
  
 Para definições de função, você só pode excluir os que não são usados ativamente em uma atribuição de função. Se você tentar excluir uma função atualmente em uso, o servidor de relatório não excluirá a função e uma mensagem de erro será exibida. Se a página contiver uma única definição de função que não está atualmente em uso, ela será excluída quando você clicar em **OK**. Se esta página contiver várias funções, você não poderá selecionar quais funções serão mantidas ou removidas. Todas as definições de função não usadas serão excluídas quando você clicar em **OK**.  
  
 Uma operação de exclusão não pode ser desfeita. Para recuperar um item excluído, recrie-o ou restaure uma cópia de backup do banco de dados do servidor de relatório.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome do item que você está excluindo.  
  
 **Tipo**  
 Exibe o tipo de item que você está excluindo.  
  
 **Proprietário**  
 Exibe o nome do proprietário. Na maioria dos casos é o Sistema.  
  
 **Status**  
 Exibe informações de andamento de uma operação de exclusão.  
  
 **Erro**  
 Exibe um código de erro se um erro ocorrer durante a exclusão de um item.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir um item &#40;Management Studio&#41;](delete-an-item-management-studio.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Criar, modificar e excluir agendas](../subscriptions/create-modify-and-delete-schedules.md)  
  
  
