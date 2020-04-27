---
title: Propriedades de configuração do SQL Server Native Client (guia Sinalizadores) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bf95081d3c4657dd147e06ae54d413dd96c4c18
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63028284"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>Propriedades de configuração do SQL Server Native Client (guia Sinalizadores)
  Os clientes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador comunicam-se com servidores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os protocolos fornecidos no arquivo de biblioteca do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Esta página fornece as configurações do computador cliente para solicitar uma conexão criptografada usando SSL. Se uma conexão criptografada não puder ser estabelecida, a conexão falhará.  
  
 O processo de logon sempre é criptografado. As opções a seguir só se aplicam a dados de criptografia. Para obter mais informações sobre como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criptografa a comunicação e obter instruções sobre como configurar o cliente para confiar na autoridade raiz do certificado do servidor, consulte "Criptografando conexões com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" e "Como habilitar conexões criptografadas no [!INCLUDE[ssDE](../../includes/ssde-md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Forçar criptografia de protocolo**  
 Solicitar uma conexão usando SSL.  
  
 **Confiar em Certificado do Servidor**  
 Quando definido como **Não**, o processo de cliente tenta validar o certificado do servidor. O cliente e o servidor devem ter um certificado emitido por uma autoridade de certificação pública. Se o certificado não estiver presente no computador cliente, ou se a validação do certificado falhar, a conexão será encerrada.  
  
 Quando definido como **Sim**, o cliente não valida o certificado do servidor, portanto permitindo o uso de um certificado autoassinado.  
  
 **Confiar em Certificado do Servidor** só estará disponível se a opção **Forçar criptografia de protocolo** for definida como **Sim**.  
  
  
