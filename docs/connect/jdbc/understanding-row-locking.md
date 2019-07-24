---
title: Noções básicas sobre o bloqueio de linha | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a2d4faf6f66942cb8f1053bd7323a77795229d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916618"
---
# <a name="understanding-row-locking"></a>Entendendo bloqueio de linha

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa bloqueios de linha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses bloqueios implementam controles de simultaneidade entre vários usuários que estão realizando modificações em um banco de dados ao mesmo tempo. Por padrão, as transações e os bloqueios são gerenciados por conexão. Por exemplo, se um aplicativo abrir duas conexões JDBC, os bloqueios adquiridos por uma conexão não poderão ser compartilhados com a outra conexão. Nenhuma conexão pode adquirir bloqueios que estariam em conflito com bloqueios mantidos pela outra conexão.

> [!NOTE]  
> Se bloqueio de linha for usado, serão bloqueadas todas as linhas no buffer de busca, de modo que uma configuração muito grande para o tamanho da busca pode afetar a simultaneidade.

O bloqueio é usado para garantir a integridade transacional e a consistência do banco de dados. O bloqueio impede que os usuários leiam dados que estão sendo alterados por outros usuários e impedem que vários usuários alterem os mesmos dados ao mesmo tempo. Se o bloqueio não for usado, os dados dentro do banco de dados poderão se tornar logicamente incorretos e as consultas executadas naqueles dados podem gerar resultados inesperados.

> [!NOTE]  
> Para obter mais informações sobre bloqueio de linha no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja "Bloqueando no [!INCLUDE[ssDE](../../includes/ssde_md.md)]" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Consulte Também

[Gerenciando conjuntos de resultados com o JDBC Driver](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)
