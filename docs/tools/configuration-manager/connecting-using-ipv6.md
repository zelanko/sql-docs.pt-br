---
title: Conectando-se com o IPv6 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 02be74463da560da23ee016918a17bc0d272319d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-using-ipv6"></a>Conectando com o uso de IPv6
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dar suporte total ao protocolo IP versão 4 (IPv4) e protocolo IP versão 6 (IPv6). Quando o Windows é configurado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]IPv6, os componentes reconhecem automaticamente a existência do IPv6. Nenhuma configuração especial do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária.  
  
 O suporte abrange, mas não se limita aos seguintes itens:  
  
-   O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e os outros componentes de servidor podem escutar nos endereços IPv4 e IPv6 ao mesmo tempo. Quando tanto IPv4 quanto IPv6 estão presentes, é possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para configurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para escutar somente em endereços IPv4 ou somente em endereços IPv6.  
  
-   Quando o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado em uma máquina que dá suporte tanto para IPv4 quanto para IPv6 é consultado sobre um endereço IPv4, ele responde com um endereço IPv4 e a primeira porta TCP do IPv4 da sua lista. Quando consultado sobre um endereço IPv6, ele responde com um endereço IPv6 e a primeira porta TCP do IPv6 da sua lista. Para evitar inconsistência, é recomendável que os ouvintes de IPv4 e IPv6 sejam configurados para escutar na mesma porta.  
  
-   Ferramentas como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager aceitam os formatos IPv4 e IPv6 para endereços IP. Na maioria dos casos, a cadeia de caracteres de conexão não precisará ser modificada se o \< *nome_do_computador*>\\<*instance_name*> é especificado usando o nome do servidor host ou nome de domínio totalmente qualificado (FQDN). Se o servidor tiver IPv4 e IPv6, seu nome de host ou FQDN será resolvido como vários endereços IP, inclusive pelo menos um endereço IPv4 e vários endereços IPv6. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client tenta estabelecer conexões usando esses endereços IP na ordem recebida do TCP/IP e usa a primeira conexão que é bem-sucedida. Como a ordem não pode ser prevista pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, ela é considerada uma ordem aleatória. Serão tentados endereços IPv4 primeiro se os endereços IPv4 e IPv6 estiverem presentes. Essa lógica é transparente para os usuários de ODBC, OLE DB ou ADO.NET.  
  
    > [!NOTE]  
    >  Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não estiver escutando no IPv4, a conexão IPv4 tentada deverá aguardar o período do tempo limite para que o endereço IPv6 seja tentado. Para evitar isso, conecte-se diretamente ao endereço IP IPv6 ou configure um alias no cliente com o endereço IPv6.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  

