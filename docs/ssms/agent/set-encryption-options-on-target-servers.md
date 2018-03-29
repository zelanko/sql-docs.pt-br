---
title: Definir opções de criptografia em servidores de destino | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 605078d66a1ee247df8d977a190316c340d9a1f9
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="set-encryption-options-on-target-servers"></a>Definir opções de criptografia em servidores de destino
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Se você não puder usar um certificado para comunicações criptografadas em SSL (Secure Sockets Layer) entre os servidores mestres e parte ou todos os servidores de destino, mas quiser criptografar o canal entre eles, configure o servidor de destino para que use o nível de segurança necessário.  
  
Para configurar o nível apropriado de segurança necessário para um canal de comunicação servidor mestre/servidor de destino específico, defina a subchave do Registro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*instance_name*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** no servidor de destino como um dos valores a seguir. O valor de \<*instance_name*> é **MSSQL.***n*. Por exemplo, **MSSQL.1** ou **MSSQL.3**.  
  
|Valor|Description|  
|---------|---------------|  
|**0**|Desabilita a criptografia entre este servidor de destino e o servidor mestre. Escolha esta opção apenas quando o canal entre o servidor de destino e servidor mestre estiver protegido por outros meios.|  
|**1**|Habilita criptografia apenas entre este servidor de destino e o servidor mestre, mas nenhuma validação de certificado é necessária.|  
|**2**|Habilita criptografia SSL completa e validação de certificado entre este servidor de destino e o servidor mestre. Esta é a configuração padrão. A menos que haja um motivo específico para escolher um valor diferente, nós recomendamos não alterá-la.|  
  
Se **1** ou **2** for especificado, SSL deverá estar habilitado em ambos os servidores, mestre e de destino. Se **2** for especificado, também será necessário haver um certificado apropriadamente assinado no servidor mestre.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>Consulte Também  
[Como habilitar conexões criptografadas no Mecanismo de Banco de Dados (SQL Server Configuration Manager)](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006)  
  
