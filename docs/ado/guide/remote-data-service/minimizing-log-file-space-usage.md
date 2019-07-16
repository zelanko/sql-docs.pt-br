---
title: Minimizar o uso de espaço do arquivo de Log | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8dc0799fbeba24ad4725d25647ef471edad8fb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922553"
---
# <a name="minimizing-log-file-space-usage"></a>Minimizar o uso de espaço de arquivo de log
Um arquivo de log pode se esgotar rapidamente (parada, portanto, o servidor) se não houver um grande volume de atividade em um banco de dados do SQL Server. Você pode definir o arquivo de log para **truncar no ponto de verificação** significativamente estender a vida útil do arquivo de log para um banco de dados.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Para habilitar truncar no ponto de verificação no Microsoft SQL Server 6.5  
  
1.  Iniciar o Microsoft SQL Server Enterprise Manager, abra a árvore para o servidor e, em seguida, abrir a árvore de dispositivos de banco de dados.  
  
2.  Clique duas vezes o nome do banco de dados no qual esse recurso será habilitado.  
  
3.  Dos **banco de dados** guia, selecione **Truncate**.  
  
4.  Dos **opções** guia, selecione **truncar Log no ponto de verificação**e, em seguida, clique em **Okey**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Para habilitar truncar no ponto de verificação no Microsoft SQL Server 7.0  
  
1.  Iniciar o Microsoft SQL Server Enterprise Manager, abra a árvore para o servidor e, em seguida, abrir a árvore de bancos de dados.  
  
2.  Clique no nome do banco de dados no qual esse recurso será habilitado e escolha **propriedades**.  
  
3.  Dos **opções** guia, selecione **truncar Log no ponto de verificação**e, em seguida, clique em **Okey**.  
  
 Para obter mais informações sobre o **truncar no ponto de verificação** de recursos, consulte a documentação do Microsoft SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


