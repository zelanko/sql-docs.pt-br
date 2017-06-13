---
title: rsInternalError - erro do Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsInternalError
ms.assetid: 52613d52-fc78-4870-93f0-7d393ab9c335
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7265597c2376d62b6d3e42c55c8d87e45f6d869e
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="rsinternalerror---reporting-services-error"></a>rsInternalError - Erro do Reporting Services
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsInternalError|  
|Origem do evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|Um erro interno ocorreu no servidor de relatório. Consulte o log de erros para obter mais detalhes.|  
  
## <a name="explanation"></a>Explicação  
 Essa é uma mensagem de erro genérica seguida frequentemente por um erro mais descritivo que fornece mais detalhes.  
  
 Erros internos são incomuns. Se esse erro for exibido, mais informações estarão disponíveis nos logs de rastreamento de servidor de relatório. Além disso, se estiver executando como administrador local no mesmo computador em que ocorreu o erro, será possível exibir a pilha de chamadas para obter mais informações.  
  
## <a name="user-action"></a>Ação do usuário  
 Para determinar a causa específica para essa mensagem, examine os arquivos de log de servidor de relatório, localizados em \Microsoft SQL Server\MSRS12. \<instancename > \reporting. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
 Para exibir a pilha de chamadas, clique com o botão direito do mouse na página em que ocorreu o erro e aponte para **Exibir Código-Fonte**. A exibição da pilha de chamadas exige permissões de administrador no mesmo computador em que o erro ocorreu.  
  
 Se não houver nenhuma informação adicional disponível, será possível tentar a solicitação novamente.  
  
## <a name="internal-only"></a>Somente interno  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
