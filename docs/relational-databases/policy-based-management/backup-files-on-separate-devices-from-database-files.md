---
title: Os arquivos de backup precisam estar em dispositivos separados dos arquivos de banco de dados
description: Saiba como habilitar uma política para verificar a localização do arquivo de backup comparado à localização do arquivo de banco de dados para o gerenciamento baseado em políticas com o SQL Server.
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 5b98f8163a3564ccc4aadac6c71c30eb5cf37697
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284881"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>Os arquivos de backup precisam estar em dispositivos separados dos arquivos de banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica se os arquivos de banco de dados estão em dispositivos separados dos arquivos de backup. Se os arquivos de banco de dados e os arquivos de backup estiverem no mesmo dispositivo e o dispositivo falhar, o banco de dados e os backups não estarão disponíveis. Além disso, colocar arquivos de banco de dados e de backup em dispositivos separados otimiza o desempenho de E/S para o uso de produção do banco de dados e a gravação de backups.  
  
## <a name="best-practices-recommendations"></a>Recomendações de melhores práticas  
 Nós recomendamos que um disco de backup seja diferente dos discos de banco de dados e de log. Isso é necessário para garantir que será possível acessar os backups se houver falha no disco de dados ou de log.

Se os arquivos de banco de dados e os arquivos de backup estiverem no mesmo dispositivo e o dispositivo falhar, o banco de dados e os backups não estarão disponíveis. Além disso, colocar arquivos de banco de dados e de backup em dispositivos separados otimiza o desempenho de E/S para o uso de produção do banco de dados e a gravação de backups.
  
## <a name="see-also"></a>Confira também 
   
  
 [Dispositivos de backup](../backup-restore/backup-devices-sql-server.md)  
  
