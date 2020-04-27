---
title: Protocolos para propriedades MSSQLSERVER (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9000dd2b7456036f4828640694aaf697036b71d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62645797"
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>Protocolos para propriedades de MSSQLSERVER (guia Avançado)
  Use a guia **Avançado** na caixa de diálogo **Protocolos para Propriedades de MSSQLSERVER** para configurar a **Proteção Estendida para Autenticação** para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. A**Proteção Estendida** é um recurso dos componentes de rede implementado pelo sistema operacional. A**Proteção Estendida** está disponível no Windows 7 e no Windows Server 2008 R2 e está incluída em service packs de sistemas operacionais anteriores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mais seguro quando as conexões são efetuadas usando a **Proteção Estendida**. Alguns benefícios da **Proteção Estendida** exigem a seleção de **Forçar Criptografia** na guia **Sinalizadores** .  
  
> [!IMPORTANT]  
>  O Windows não habilita a **Proteção Estendida** por padrão. Para obter informações sobre como habilitar a **Proteção Estendida** no Windows, consulte o artigo [Proteção Estendida para Autenticação](https://go.microsoft.com/fwlink/?LinkId=178431)na Base de Dados de Conhecimento.  
  
 Para obter mais informações sobre como configurar outros serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e uma descrição completa da **Proteção Estendida**, consulte informações mais recentes em [Microsoft.com](https://go.microsoft.com/fwlink/?LinkId=177752).  
  
 A**Proteção Estendida** tem suporte completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client a partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Não há suporte para a **Proteção Estendida** para outros provedores de cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualmente.  
  
## <a name="options"></a>Opções  
 **Proteção Estendida**  
 Há três valores possíveis:  
  
-   Quando definida como **Ativada**, a **Proteção Estendida** está desabilitada. A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitará conexões de qualquer cliente, independentemente de o cliente estar protegido ou não. A opção**Desativada** é compatível com sistemas operacionais mais antigos e sem patches, mas é menos segura. Só use essa configuração se souber que os sistemas operacionais cliente não têm suporte para proteção estendida.  
  
-   Quando definida como **Permitida**, a **Proteção Estendida** é necessária para conexões de sistemas operacionais com suporte para a **Proteção Estendida**. As conexões de aplicativos cliente desprotegidos que estejam sendo executados em sistemas operacionais cliente protegidos são rejeitadas. A**Proteção Estendida** é ignorada para conexões de sistemas operacionais desprotegidos. Essa configuração é mais segura que **Desativada**, mas não é a configuração mais segura. Use essa configuração em ambientes mistos, onde alguns sistemas operacionais ou aplicativos dão suporte à **Proteção Estendida** e outros não.  
  
-   Quando definida como **Obrigatória**, somente conexões de aplicativos protegidos em sistemas operacionais protegidos são aceitas. Essa configuração é a mais segura dentre as três, mas conexões de sistemas operacionais sem suporte para **Proteção Estendida** não poderão ser estabelecidas com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **SPNs NTLM aceitos**  
 Quando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for identificada por mais de um SPN (nome principal do serviço) de NTLM, liste os SPNs aqui como uma série de cadeias de caracteres separadas por ponto-e-vírgula. Por exemplo, o valor **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**indica que clientes que tentam se conectar a SPNs nomeados **MSSQLSvc/HOST1.Contoso.com** e **MSSQLSvc/HOST2.Contoso.com** são permitidos. Essa variável tem um tamanho máximo de 2.048 caracteres.  
  
## <a name="see-also"></a>Consulte Também  
 [Proteção Estendida para Autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
