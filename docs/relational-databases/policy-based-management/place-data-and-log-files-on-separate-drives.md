---
title: Colocar arquivos de dados e de log em unidades separadas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54f469f8ab9f0daaf6f37c8f6bad1878bc716dbd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086934"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>Colocar arquivos de dados e de log em unidades separadas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se os arquivos de dados e de log são colocados em unidades lógicas separadas. Colocar arquivos de dados E de log no mesmo dispositivo pode causar contenção para esse dispositivo e resultar em um baixo desempenho. Colocar os arquivos em unidades separadas permite que a atividade de E/S ocorra ao mesmo tempo para os arquivos de dados e de log.  
  
## <a name="recommendations"></a>Recomendações  
 Ao criar um novo banco de dados novo, especifique unidades separadas para os dados e o log. Para mover os arquivos depois que o banco de dados é criado, o banco de dados deve ser usado offline. Mova os arquivos usando um dos seguintes métodos:  
  
> [!NOTE]  
>  Essa política não pode detectar dispositivos físicos separados por pontos de montagem  
  
-   Restaure o banco de dados do backup usando a instrução RESTORE DATABASE com a opção WITH MOVE.  
  
-   Desanexe e, em seguida, anexe o banco de dados especificando locais separados para os dispositivos de dados e de log.  
  
-   Especifique um novo local executando a instrução ALTER DATABASE com a opção MODIFY FILE e, em seguida, reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Mover arquivos de banco de dados](../../relational-databases/databases/move-database-files.md)  
  
 [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md)  
  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
