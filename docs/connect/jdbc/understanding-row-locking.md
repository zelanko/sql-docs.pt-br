---
title: Noções básicas sobre bloqueio de linha | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cdf5ca943ec4d823c8c568f0818a49c44f22cbe6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040774"
---
# <a name="understanding-row-locking"></a>Entendendo bloqueio de linha
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa bloqueios de linha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses bloqueios implementam controle de simultaneidade entre vários usuários que estão realizando modificações em um banco de dados ao mesmo tempo. Por padrão, as transações e os bloqueios são gerenciados por conexão. Por exemplo, se um aplicativo abrir duas conexões JDBC, os bloqueios adquiridos por uma conexão não poderão ser compartilhados com a outra conexão. Nenhuma conexão pode adquirir bloqueios que estariam em conflito com bloqueios mantidos pela outra conexão.  
  
> [!NOTE]  
>  Se bloqueio de linha for usado, serão bloqueadas todas as linhas no buffer de busca, de modo que uma configuração muito grande para o tamanho da busca pode afetar a simultaneidade.  
  
 O bloqueio é usado para garantir a integridade transacional e a consistência do banco de dados. O bloqueio impede que os usuários leiam dados que estão sendo alterados por outros usuários e impedem que vários usuários alterem os mesmos dados ao mesmo tempo. Se o bloqueio não for usado, os dados dentro do banco de dados poderão se tornar logicamente incorretos e as consultas executadas naqueles dados podem gerar resultados inesperados.  
  
> [!NOTE]  
>  Para obter mais informações sobre bloqueio de linha no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], veja "Bloqueando no [!INCLUDE[ssDE](../../includes/ssde_md.md)]" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando conjuntos de resultados com o JDBC Driver](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
