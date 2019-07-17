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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135643"
---
# <a name="data-source-example"></a>Exemplo de fonte de dados
Em computadores que executam o Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT da estação de trabalho/Windows 2000 Professional ou Microsoft Windows® 95/98, dados da máquina informações de origem são armazenadas no registro. Dependendo de qual registro chave as informações são armazenadas em, a fonte de dados é conhecida como um *fonte de dados de usuário* ou um *fonte de dados do sistema*. Fontes de dados do usuário são armazenadas na chave HKEY_CURRENT_USER e estão disponíveis somente para o usuário atual. Fontes de dados do sistema são armazenadas na chave HKEY_LOCAL_MACHINE e podem ser usadas por mais de um usuário em um único computador. Eles também podem ser usados pelos serviços de todo o sistema, que podem então obter acesso à fonte de dados, mesmo se nenhum usuário está conectado à máquina. Para obter mais informações sobre fontes de dados do sistema e de usuário, consulte [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Suponha que um usuário tem três fontes de dados de usuário: Pessoal e o inventário, que usam um DBMS Oracle; e a folha de pagamento, que usa um DBMS do Microsoft SQL Server. Os valores do registro para fontes de dados podem ser:  
  
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
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
