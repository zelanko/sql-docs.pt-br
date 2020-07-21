---
title: MSSQLSERVER_-1 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ed9c25be4a4e3cfa6b0c00c9dc790214415d3593
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554231"
---
# <a name="mssqlserver_-1"></a>MSSQLSERVER_-1
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|-1|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro ao estabelecer uma conexão com o servidor.  Ao estabelecer conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essa falha pode ser causada pelo fato de que as configurações padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permitem conexões remotas. (provedor: adaptadores de rede do SQL, erro: 28 – O servidor não é compatível com o protocolo solicitado) (Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], erro: -1)|  
  
## <a name="explanation"></a>Explicação  
 O cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar com o servidor. Esse erro pode ser causado por um dos seguintes motivos:  
  
-   Um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado é inválido.  
  
-   O TCP ou protocolos de pipes nomeados não estão habilitados.  
  
-   O firewall no servidor recusou a conexão.  
  
-   O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sqlbrowser) não foi iniciado.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver esse erro, tente uma das seguintes ações:  
  
-   Verifique a ortografia do nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é especificado na cadeia de conexão.  
  
-   Use a ferramenta Configuration Manager do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceite conexões remotas pelo protocolo TCP ou de pipes nomeados.  
  
-   Verifique se você configurou o firewall na instância de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para abrir portas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a porta do Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (UDP 1434).  
  
-   Certifique-se de que o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha sido iniciado no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um firewall do Windows para acesso Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Configuração de rede do cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)   
 [Habilitar ou desabilitar um protocolo de rede do servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
