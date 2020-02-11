---
title: Exemplo de fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec9eacef6f0bd63eb0aaeac36dc97938297d1f16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135643"
---
# <a name="data-source-example"></a>Exemplo de fonte de dados
Em computadores que executam o Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional ou Microsoft Windows® 95/98, as informações da fonte de dados do computador são armazenadas no registro. Dependendo de qual chave do registro as informações são armazenadas, a fonte de dados é conhecida como uma *fonte de dados do usuário* ou uma *fonte de dados do sistema*. As fontes de dados do usuário são armazenadas na chave HKEY_CURRENT_USER e estão disponíveis somente para o usuário atual. As fontes de dados do sistema são armazenadas sob a chave de HKEY_LOCAL_MACHINE e podem ser usadas por mais de um usuário em uma máquina. Eles também podem ser usados por serviços de todo o usuário, que podem, então, obter acesso à fonte de dados, mesmo que não haja usuários conectados à máquina. Para obter mais informações sobre fontes de dados do usuário e do sistema, consulte [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Suponha que um usuário tenha três fontes de dados de usuário: pessoal e inventário, que usam um DBMS Oracle; e folha de pagamento, que usa um Microsoft SQL Server DBMS. Os valores de registro para fontes de dados podem ser:  
  
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
  
 e os valores do registro para a fonte de dados da folha de pagamento podem ser:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
