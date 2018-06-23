---
title: Arquivos de backup devem ser em dispositivos separados dos arquivos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 777ce42b33fea98b3770e3fc073cf1f76b3814fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005698"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>Arquivos de backup devem estar em dispositivos separados dos arquivos de banco de dados
  Esta regra verifica se os arquivos de banco de dados estão em dispositivos separados dos arquivos de backup. Se os arquivos de banco de dados e os arquivos de backup estiverem no mesmo dispositivo e o dispositivo falhar, o banco de dados e os backups não estarão disponíveis. Além disso, colocar arquivos de banco de dados e de backup em dispositivos separados otimiza o desempenho de E/S para o uso de produção do banco de dados e a gravação de backups.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 É extremamente recomendável que você coloque o banco de dados e os backups em dispositivos de backup separados.  
  
> [!NOTE]  
>  Essa política não pode detectar dispositivos físicos separados por pontos de montagem.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Dispositivos de backup &#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [Fazer backup e restaurar bancos de dados do SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  