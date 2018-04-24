---
title: Minimizar o uso de espaço de arquivo de Log | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b333875afe103eb0438b567666e54c9985c51997
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="minimizing-log-file-space-usage"></a>Minimizar o uso de espaço de arquivo de Log
Um arquivo de log pode preencher rapidamente (interrupção, portanto, o servidor) se houver um grande volume de atividade em um banco de dados do SQL Server. Você pode definir o arquivo de log para **Truncate no ponto de verificação** significativamente estender a vida útil do arquivo de log para um banco de dados.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Para habilitar Truncate no ponto de verificação no Microsoft SQL Server 6.5  
  
1.  Iniciar o Microsoft SQL Server Enterprise Manager, abra a árvore para o servidor e, em seguida, abra a árvore de dispositivos de banco de dados.  
  
2.  Clique duas vezes no nome do banco de dados no qual este recurso será habilitado.  
  
3.  Do **banco de dados** guia, selecione **Truncate**.  
  
4.  Do **opções** guia, selecione **truncar o Log no ponto de verificação**e, em seguida, clique em **Okey**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Para habilitar Truncate no ponto de verificação no Microsoft SQL Server 7.0  
  
1.  Iniciar o Microsoft SQL Server Enterprise Manager, abra a árvore para o servidor e, em seguida, abra a árvore de bancos de dados.  
  
2.  Clique no nome do banco de dados no qual este recurso será habilitado e escolha **propriedades**.  
  
3.  Do **opções** guia, selecione **truncar o Log no ponto de verificação**e, em seguida, clique em **Okey**.  
  
 Para obter mais informações sobre o **Truncate no ponto de verificação** de recursos, consulte a documentação do Microsoft SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


