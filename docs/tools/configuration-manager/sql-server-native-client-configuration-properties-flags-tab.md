---
title: "Propriedades de configuração do SQL Server Native Client (guia sinalizadores) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5d9175bba7e492ad2844803a8ce7fe1e6c09034
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>Propriedades de configuração do SQL Server Native Client (guia Sinalizadores)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clientes nesta máquina se comunicam com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servidores usando os protocolos fornecidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de biblioteca do Native Client. Esta página fornece as configurações do computador cliente para solicitar uma conexão criptografada usando SSL. Se uma conexão criptografada não puder ser estabelecida, a conexão falhará.  
  
 O processo de logon sempre é criptografado. As opções a seguir só se aplicam a dados de criptografia. Para obter mais informações sobre como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criptografa a comunicação e obter instruções sobre como configurar o cliente para confiar na autoridade raiz do certificado do servidor, consulte "Criptografando conexões com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" e "Como habilitar conexões criptografadas no [!INCLUDE[ssDE](../../includes/ssde-md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Forçar criptografia de protocolo**  
 Solicitar uma conexão usando SSL.  
  
 **Confiar em Certificado do Servidor**  
 Quando definido como **Não**, o processo de cliente tenta validar o certificado do servidor. O cliente e o servidor devem ter um certificado emitido por uma autoridade de certificação pública. Se o certificado não estiver presente no computador cliente, ou se a validação do certificado falhar, a conexão será encerrada.  
  
 Quando definido como **Sim**, o cliente não valida o certificado do servidor, portanto permitindo o uso de um certificado autoassinado.  
  
 **Confiar em Certificado do Servidor** só estará disponível se a opção **Forçar criptografia de protocolo** for definida como **Sim**.  
  
  
