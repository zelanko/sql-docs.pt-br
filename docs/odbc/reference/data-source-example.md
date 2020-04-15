---
title: Exemplo de Fonte de Dados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306517"
---
# <a name="data-source-example"></a>Exemplo de fonte de dados
Nos computadores que executam o Microsoft® o Windows NT® Server/Windows 2000 Server, o Microsoft Windows NT Workstation/Windows 2000 Professional ou o Microsoft Windows® 95/98, as informações de origem de dados da máquina são armazenadas no registro. Dependendo da chave de registro em que as informações são armazenadas, a fonte de dados é conhecida como fonte de *dados do usuário* ou fonte de dados do *sistema.* As fontes de dados do usuário são armazenadas sob a chave HKEY_CURRENT_USER e estão disponíveis apenas para o usuário atual. As fontes de dados do sistema são armazenadas sob a chave HKEY_LOCAL_MACHINE e podem ser usadas por mais de um usuário em uma máquina. Eles também podem ser usados por serviços de todo o sistema, que podem então obter acesso à fonte de dados, mesmo que nenhum usuário esteja conectado à máquina. Para obter mais informações sobre fontes de dados do usuário e do sistema, consulte [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Suponha que um usuário tenha três fontes de dados do usuário: Pessoal e Inventário, que usam um Oracle DBMS; e Payroll, que usa um Microsoft SQL Server DBMS. Os valores de registro para fontes de dados podem ser:  
  
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
  
 e os valores de registro para a fonte de dados da Folha de Pagamento podem ser:  
  
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
