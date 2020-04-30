---
title: Propriedades de configuração do SQL Server Native Client (guia Sinalizadores)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 4d8fd24d496c9a9fd42422aa9e46d26ddb27f062
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087438"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>Propriedades de configuração do SQL Server Native Client (guia Sinalizadores)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Os clientes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador comunicam-se com servidores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os protocolos fornecidos no arquivo de biblioteca do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Esta página fornece as configurações do computador cliente para solicitar uma conexão criptografada usando protocolo TLS, anteriormente conhecido como protocolo SSL. Se uma conexão criptografada não puder ser estabelecida, a conexão falhará.  
  
 O processo de logon sempre é criptografado. As opções a seguir só se aplicam a dados de criptografia. Para obter mais informações sobre como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criptografa a comunicação e para obter instruções sobre como configurar o cliente para confiar na autoridade raiz do certificado do servidor, confira "Como criptografar conexões para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" e "Como: habilitar conexões criptografadas para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Gerenciador de Configurações)" no Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Forçar criptografia de protocolo**  
 Solicite uma conexão usando TLS.  
  
 **Confiar em Certificado do Servidor**  
 Quando definido como **Não**, o processo de cliente tenta validar o certificado do servidor. O cliente e o servidor devem ter um certificado emitido por uma autoridade de certificação pública. Se o certificado não estiver presente no computador cliente, ou se a validação do certificado falhar, a conexão será encerrada.  
  
 Quando definido como **Sim**, o cliente não valida o certificado do servidor, portanto permitindo o uso de um certificado autoassinado.  
  
 **Confiar em Certificado do Servidor** só estará disponível se a opção **Forçar criptografia de protocolo** for definida como **Sim**.  
  
  
