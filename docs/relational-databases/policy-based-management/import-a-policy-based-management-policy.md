---
title: Importar uma política do Gerenciamento Baseado em Políticas | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54e0ca12595b0ce8bdde128c9261918c910ffdcf
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934340"
---
# <a name="import-a-policy-based-management-policy"></a>Importar política de Gerenciamento Baseado em Políticas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como importar uma instância de Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="permissions"></a>Permissões
 Requer a associação à função PolicyAdministratorRole no banco de dados msdb.

  
##  <a name="using-sql-server-management-studio"></a>Como usar o SQL Server Management Studio.  
  
### <a name="to-import-a-policy-instance"></a>Para importar uma instância de política  
  
1.  No painel **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor em que a instância de política recém-importada residirá.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique no sinal de adição para expandir a pasta **Gerenciamento de Política**.  
  
4.  Clique com o botão direito do mouse na pasta **Políticas** e selecione **Importar Política**.  
  
5.  Na caixa de diálogo **Importar** , digite o caminho e o nome do arquivo ou use o botão Procurar (**...**) para localizar o arquivo XML que contém a política e selecione o arquivo. Para obter mais informações sobre as opções disponíveis na caixa de diálogo **Importar** , consulte [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md).  
  
6.  Quando terminar, clique em **OK**.  


## <a name="example-policies"></a>Exemplo de políticas
 Os exemplos de políticas não são incluídos no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], mas os exemplos anteriores de políticas distribuídas podem ser acessados pela instalação do [SQL Server Management Studio v17](../../ssms/release-notes-ssms.md#previous-ssms-releases).  Após a instalação do SQL Server Management Studio v17, encontre os exemplos de políticas em `C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Policies`. Essas políticas podem ser importadas e usadas como base para as próprias políticas de gerenciamento baseado em políticas.
