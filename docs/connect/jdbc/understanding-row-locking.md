---
title: "Noções básicas sobre o bloqueio de linha | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c37c5ab29f67d7ce30603c4609cb66d3e625c61
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-row-locking"></a>Entendendo bloqueio de linha
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bloqueios de linha. Esses bloqueios implementam controle de simultaneidade entre vários usuários que estão realizando modificações em um banco de dados ao mesmo tempo. Por padrão, as transações e os bloqueios são gerenciados por conexão. Por exemplo, se um aplicativo abrir duas conexões JDBC, os bloqueios adquiridos por uma conexão não poderão ser compartilhados com a outra conexão. Nenhuma conexão pode adquirir bloqueios que estariam em conflito com bloqueios mantidos pela outra conexão.  
  
> [!NOTE]  
>  Se bloqueio de linha for usado, serão bloqueadas todas as linhas no buffer de busca, de modo que uma configuração muito grande para o tamanho da busca pode afetar a simultaneidade.  
  
 O bloqueio é usado para garantir a integridade transacional e a consistência do banco de dados. O bloqueio impede que os usuários leiam dados que estão sendo alterados por outros usuários e impedem que vários usuários alterem os mesmos dados ao mesmo tempo. Se o bloqueio não for usado, os dados dentro do banco de dados poderão se tornar logicamente incorretos e as consultas executadas naqueles dados podem gerar resultados inesperados.  
  
> [!NOTE]  
>  Para obter mais informações sobre bloqueio de linha no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte "bloqueando no [!INCLUDE[ssDE](../../includes/ssde_md.md)]" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conjuntos de resultados com o JDBC Driver](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
