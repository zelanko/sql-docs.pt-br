---
title: Exemplo de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19e5596107f5bae9ceeab8ae105203e89584e854
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-example"></a>Exemplo de fonte de dados
Em computadores que executam o Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional ou Microsoft Windows® 95/98, dados de máquina, informações de origem são armazenadas no registro. Dependendo de qual registro chave as informações são armazenadas em, a fonte de dados é conhecida como um *fonte de dados de usuário* ou um *fonte de dados do sistema*. Fontes de dados do usuário são armazenadas na chave HKEY_CURRENT_USER e estão disponíveis somente para o usuário atual. Fontes de dados do sistema são armazenados na chave HKEY_LOCAL_MACHINE e podem ser usados por mais de um usuário em um computador. Eles também podem ser usados pelos serviços de todo o sistema, que podem então obter acesso à fonte de dados mesmo se nenhum usuário estiver conectado ao computador. Para obter mais informações sobre fontes de dados do sistema e de usuário, consulte [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Suponha que um usuário tem três fontes de dados do usuário: pessoal e inventário, que usam um DBMS Oracle; e a folha de pagamento, que usa um DBMS do Microsoft SQL Server. Os valores do registro para fontes de dados podem ser:  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 e os valores do registro para a fonte de dados de folha de pagamento podem ser:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
