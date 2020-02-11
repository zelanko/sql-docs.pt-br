---
title: Conectando usando IPv6 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db26351430c6b7e0737273b2107bea242c455a2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63253777"
---
# <a name="connecting-using-ipv6"></a>Conectando com o uso de IPv6
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dão suporte total ao protocolo IP versão 4 (IPv4) e versão 6 (IPv6). Quando o Windows é configurado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]IPv6, os componentes reconhecem automaticamente a existência do IPv6. Nenhuma configuração especial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária.  
  
 O suporte abrange, mas não se limita aos seguintes itens:  
  
-   O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e os outros componentes de servidor podem escutar nos endereços IPv4 e IPv6 ao mesmo tempo. Quando tanto IPv4 quanto IPv6 estão presentes, é possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para configurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para escutar somente em endereços IPv4 ou somente em endereços IPv6.  
  
-   Quando o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado em uma máquina que dá suporte tanto para IPv4 quanto para IPv6 é consultado sobre um endereço IPv4, ele responde com um endereço IPv4 e a primeira porta TCP do IPv4 da sua lista. Quando consultado sobre um endereço IPv6, ele responde com um endereço IPv6 e a primeira porta TCP do IPv6 da sua lista. Para evitar inconsistência, é recomendável que os ouvintes de IPv4 e IPv6 sejam configurados para escutar na mesma porta.  
  
-   Ferramentas como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager aceitam os formatos IPv4 e IPv6 para endereços IP. Na maioria dos casos, a cadeia de conexão não precisará ser modificada se o \<*computer_name*>\\<*instance_name*> for especificado usando o nome do host do servidor ou o FQDN (nome de domínio totalmente qualificado). Se o servidor tiver IPv4 e IPv6, seu nome de host ou FQDN será resolvido como vários endereços IP, inclusive pelo menos um endereço IPv4 e vários endereços IPv6. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Native Client tenta estabelecer conexões usando esses endereços IP na ordem recebida do TCP/IP e usa a primeira conexão bem-sucedida. Como a ordem não pode ser prevista pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, ela é considerada uma ordem aleatória. Serão tentados endereços IPv4 primeiro se os endereços IPv4 e IPv6 estiverem presentes. Essa lógica é transparente para os usuários de ODBC, OLE DB ou ADO.NET.  
  
    > [!NOTE]  
    >  Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não estiver escutando no IPv4, a conexão IPv4 tentada deverá aguardar o período do tempo limite para que o endereço IPv6 seja tentado. Para evitar isso, conecte-se diretamente ao endereço IP IPv6 ou configure um alias no cliente com o endereço IPv6.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
