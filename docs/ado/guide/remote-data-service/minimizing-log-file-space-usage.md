---
title: Minimizando o uso do espaço do arquivo de log | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922553"
---
# <a name="minimizing-log-file-space-usage"></a>Minimizar o uso de espaço de arquivo de log
Um arquivo de log pode ser preenchido rapidamente (o que interrompe o servidor), se houver um grande volume de atividade em um banco de dados SQL Server. Você pode definir o arquivo de log para **truncar no ponto de verificação** para estender significativamente a vida útil do arquivo de log para um banco de dados.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>Para habilitar o truncamento no ponto de verificação no Microsoft SQL Server 6,5  
  
1.  Inicie o Gerenciador de Microsoft SQL Server Enterprise, abra a árvore para o servidor e, em seguida, abra a árvore dispositivos de banco de dados.  
  
2.  Clique duas vezes no nome do banco de dados no qual esse recurso será habilitado.  
  
3.  Na guia **banco de dados** , selecione **truncar**.  
  
4.  Na guia **Opções** , selecione **truncar log no ponto de verificação**e clique em **OK**.  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>Para habilitar o truncamento no ponto de verificação no Microsoft SQL Server 7,0  
  
1.  Inicie o Gerenciador de Microsoft SQL Server Enterprise, abra a árvore para o servidor e, em seguida, abra a árvore bancos de dados.  
  
2.  Clique com o botão direito do mouse no nome do banco de dados no qual esse recurso será habilitado e escolha **Propriedades**.  
  
3.  Na guia **Opções** , selecione **truncar log no ponto de verificação**e clique em **OK**.  
  
 Para obter mais informações sobre o recurso **truncar no ponto de verificação** , consulte a documentação do Microsoft SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


