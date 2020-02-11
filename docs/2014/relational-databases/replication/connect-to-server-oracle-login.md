---
title: Conectar ao Servidor (Oracle), Logon | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fddf6045921fa14e09aaff918f84125eb907e9ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721738"
---
# <a name="connect-to-server-oracle-login"></a>Conectar ao Servidor (Oracle), Logon
  Use a guia **logon** da caixa de diálogo **conectar ao servidor** para especificar a conta na qual as conexões são feitas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distribuidor para o Publicador Oracle. Você deve usar a mesma conta especificada para o esquema de usuário administrativo de replicação durante a configuração do Publicador. Para obter mais informações, consulte [Configure an Oracle Publisher](non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
## <a name="options"></a>Opções  
 **Instância de servidor**  
 O nome TNS (Transparent Network Substrate) do Editor Oracle, especificado durante a configuração do software cliente Oracle instalado no Distribuidor.  
  
 **Autenticação**  
 Selecione **Autenticação Padrão da Oracle** (recomendado) ou **Autenticação do Windows**. Se você selecionar **Autenticação do Windows**:  
  
-   O servidor Oracle deve ser configurado para permitir conexões que usam credenciais do Windows. Para obter mais informações, consulte a documentação Oracle.  
  
-   Você deve estar registrado atualmente na mesma conta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows especificada para o esquema de usuário administrativo de replicação.  
  
 **Logon** e **senha**  
 Se você tiver selecionado **Autenticação Padrão da Oracle** para a opção **Autenticação** , especifique o logon e a senha a serem usados, que devem ser os mesmos que os especificados para o esquema de usuário administrativo de replicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Glossário de termos para publicações Oracle](non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  
