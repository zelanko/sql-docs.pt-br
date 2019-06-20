---
title: Colocar arquivos de dados e de log em unidades separadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b957cfa6416b9c557123a235bc62832057f907c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691760"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>Colocar arquivos de dados e de log em unidades separadas
  Esta regra verifica se os arquivos de dados e de log são colocados em unidades lógicas separadas. Colocar arquivos de dados e de log no mesmo dispositivo pode causar contenção para esse dispositivo e resultar em um baixo desempenho. Colocar os arquivos em unidades separadas permite que a atividade de E/S ocorra ao mesmo tempo para os arquivos de dados e de log.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Ao criar um banco de dados novo, especifique unidades separadas para os dados e o log. Para mover os arquivos depois que o banco de dados é criado, o banco de dados deve ser usado offline. Mova os arquivos usando um dos seguintes métodos:  
  
> [!NOTE]  
>  Essa política não pode detectar dispositivos físicos separados por pontos de montagem  
  
-   Restaure o banco de dados do backup usando a instrução RESTORE DATABASE com a opção WITH MOVE.  
  
-   Desanexe e, em seguida, anexe o banco de dados especificando locais separados para os dispositivos de dados e de log.  
  
-   Especifique um novo local executando a instrução ALTER DATABASE com a opção MODIFY FILE e, em seguida, reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Mover arquivos de banco de dados](../databases/move-database-files.md)  
  
 [Mover bancos de dados de usuário](../databases/move-user-databases.md)  
  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
