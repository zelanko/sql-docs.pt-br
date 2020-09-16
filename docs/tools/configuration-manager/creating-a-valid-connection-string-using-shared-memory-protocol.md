---
title: Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada
description: Descubra quando as conexões com SQL Server usam o protocolo de memória compartilhada e como criar uma cadeia de conexão válida para esse protocolo.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e050fac6ea1b306575c5b0a9e89ef9a69d2b2293
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900519"
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  As conexões com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um cliente executado no mesmo computador usam o protocolo de memória compartilhada. A memória compartilhada não tem propriedades configuráveis. Essa memória sempre é tentada primeiro e não pode ser movida da posição superior da lista **Protocolos Habilitados** na lista **Propriedades de Protocolos de Cliente** . O protocolo de Memória Compartilhada pode ser desabilitado, o que é útil ao solucionar problemas dos outros protocolos.  
  
 Não é possível criar um alias usando o protocolo de memória compartilhada, mas se a memória compartilhada estiver habilitada, a conexão com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pelo nome criará uma conexão de memória compartilhada. Uma cadeia de conexão de memória compartilhada usa o formato `lpc:<servername>[\instancename]`.  
  
## <a name="connecting-to-the-local-server"></a>Conectando-se ao servidor local  
 Ao conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no mesmo computador que o cliente, você pode usar **(local)** como o nome do servidor. Esse procedimento não é incentivado, pois leva a ambiguidade. No entanto, ele pode ser útil quando se sabe que o cliente está sendo executado no computador pretendido. Por exemplo, ao criar um aplicativo para usuários móveis desconectados, como uma força de vendas, em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será executado em computadores laptop e armazenará dados de projeto, um cliente conectado a **(local)** sempre se conectaria ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no laptop. A palavra **localhost** ou um ponto ( **.** ) pode ser usado em lugar de **(local)** .  
  
## <a name="verifying-your-connection-protocol"></a>Verificando o protocolo de conexão  
 A consulta a seguir retornará o protocolo usado para a conexão atual.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Exemplos:  
 Os seguintes nomes se conectarão ao computador local com o protocolo da memória compartilhada, se ele estiver habilitado:  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 Não é possível criar um alias para uma conexão de memória compartilhada.  
  
> [!NOTE]  
>  A especificação de um Endereço IP na caixa **Servidor** resultará em uma conexão TCP/IP.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando uma cadeia de conexão válida usando TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Criando uma cadeia de conexão válida usando pipes nomeados](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))   
 [Escolhendo um protocolo de rede](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
