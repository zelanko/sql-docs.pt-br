---
title: rsInternalError – erro do Reporting Services | Microsoft Docs
description: 'Nesta página de referência de erro, saiba mais sobre a ID de evento "rsInternalError": Um erro interno ocorreu no servidor de relatório. Consulte o log de erros para obter mais detalhes.'
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsInternalError
ms.assetid: 52613d52-fc78-4870-93f0-7d393ab9c335
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d8df18bf9487d1d8797eff4e60f5ec5eefb87c4f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394716"
---
# <a name="rsinternalerror---reporting-services-error"></a>rsInternalError - Erro do Reporting Services
    
## <a name="details"></a>Detalhes  
  
|Categoria|Valor|  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsInternalError|  
|Origem do Evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|Um erro interno ocorreu no servidor de relatório. Consulte o log de erros para obter mais detalhes.|  
  
## <a name="explanation"></a>Explicação  
 Essa é uma mensagem de erro genérica seguida frequentemente por um erro mais descritivo que fornece mais detalhes.  
  
 Erros internos são incomuns. Se esse erro for exibido, mais informações estarão disponíveis nos logs de rastreamento de servidor de relatório. Além disso, se estiver executando como administrador local no mesmo computador em que ocorreu o erro, será possível exibir a pilha de chamadas para obter mais informações.  
  
## <a name="user-action"></a>Ação do usuário  
 Para determinar a causa específica dessa mensagem, examine os arquivos de log do servidor de relatório, localizados em \Microsoft SQL Server\MSRS12.\<instancename >\Reporting Services\LogFiles. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
 Para exibir a pilha de chamadas, clique com o botão direito do mouse na página em que ocorreu o erro e aponte para **Exibir Código-Fonte**. A exibição da pilha de chamadas exige permissões de administrador no mesmo computador em que o erro ocorreu.  
  
 Se não houver nenhuma informação adicional disponível, será possível tentar a solicitação novamente.  
  
## <a name="internal-only"></a>Somente interno  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar e parar o serviço Servidor de Relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
