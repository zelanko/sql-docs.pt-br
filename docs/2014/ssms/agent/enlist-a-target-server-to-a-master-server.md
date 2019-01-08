---
title: Inscrever um servidor de destino em um servidor mestre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3d0d91de95e82fcd174aa9290e208afda5bef91
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786208"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Inscrever um servidor de destino em um servidor mestre
  Este tópico descreve como adicionar servidores de destino a uma configuração de administração multisservidor. Execute este procedimento a partir do servidor mestre. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SMO (SQL Server Management Objects).  
  
 Para obter informações sobre como a conta do Windows usada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent afeta um ambiente multisservidor, consulte [Criar um ambiente multisservidor](create-a-multiserver-environment.md).  
  
 Criptografia SSL completa e validação de certificado encontram-se habilitadas, por padrão, para conexões entre servidores mestre e servidores de destino. Para obter mais informações, veja [Definir opções de criptografia em servidores de destino](set-encryption-options-on-target-servers.md).  
  
 **Neste tópico**  
  
-   **Para inscrever um servidor de destino, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Para inscrever um servidor de destino  
  
1.  No **Pesquisador de Objetos**, expanda um servidor que esteja configurado como servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Adicionar Servidores de Destino**.  
  
3.  Complete o Assistente de Servidor de Destino, que o guia nesse processo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Para inscrever um servidor de destino  
  
1.  Use o procedimento armazenado `sp_msx_enlist`.  Para obter mais informações, consulte [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="PowerShellProcedure"></a> Usando o SQL Server Management Objects (SMO)  
  
## <a name="see-also"></a>Consulte também  
 [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)  
  
  
