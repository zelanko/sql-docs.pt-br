---
title: Escolhendo um protocolo de rede | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 9c167994c7145bce348b6959a57533e398e1d6bb
ms.sourcegitcommit: ca9b5cb6bccfdba4cdbe1697adf5c673b4713d6c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/18/2019
ms.locfileid: "56407546"
---
# <a name="choosing-a-network-protocol"></a>Escolhendo um protocolo de rede
  Para se conectar ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , você deve ter um protocolo de rede habilitado. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode atender a solicitações em vários protocolos ao mesmo tempo. Os clientes se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um único protocolo. Se o programa cliente não souber qual protocolo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando, configure o cliente para tentar sequencialmente vários protocolos. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para habilitar, desabilitar e configurar os protocolos de rede.  
  
## <a name="shared-memory"></a>Memória compartilhada  
 A memória compartilhada é o protocolo mais simples de usar e não precisa de configurações. Como os clientes que usam o protocolo de memória compartilhada só podem se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada no mesmo computador, ele não é útil para a maior parte da atividade de banco de dados. Use o protocolo de memória compartilhada para solucionar problemas quando você suspeitar que outros protocolos estejam configurados incorretamente.  
  
> [!NOTE]  
>  Os clientes que usam MDAC 2.8 ou anterior não podem usar o protocolo de memória compartilhada. Se tentarem usar, eles serão alternados automaticamente para o protocolo de pipes nomeados.  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP é um protocolo comum amplamente utilizado na Internet. Ele faz a comunicação entre redes de computadores interconectadas que têm arquiteturas de hardware diferentes e vários sistemas operacionais. O TCP/IP contém padrões para roteamento do tráfego da rede e oferece recursos de segurança avançados. É o protocolo mais popular usado nas empresas atualmente. A configuração do computador para usar TCP/IP pode ser complexa, mas a maioria dos computadores em rede já estão configurados corretamente. Para definir as configurações de TCP/IP que não são expostas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="named-pipes"></a>Pipes nomeados  
 Pipes nomeados é um protocolo desenvolvido para redes locais. Uma parte da memória é usada por um processo a fim de passar informações para outro processo, para que a saída de um seja a entrada do outro. O segundo processo pode ser local (no mesmo computador que o primeiro) ou remoto (em um computador de rede).  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>Pipes nomeados vs. soquetes TCP/IP  
 Em um ambiente de LAN (rede local) rápida, os clientes de soquetes TCP/IP e Pipes Nomeados são comparáveis no que diz respeito ao desempenho. No entanto, a diferença de desempenho entre os clientes de Soquetes TCP/IP e Pipes Nomeados se torna aparente com redes mais lentas, como WANs (redes de longa distância) ou redes de conexão discada. Isso ocorre devido às diferentes formas de comunicação entre mecanismos IPC (comunicação entre processos) par.  
  
 Para pipes nomeados, a comunicação de rede geralmente é mais interativa. Um mecanismo par não envia dados até que outro mecanismo par os solicite usando um comando de leitura. Uma leitura de rede geralmente envolve uma série de mensagens de verificação de pipes nomeados antes que a leitura dos dados seja iniciada. Essas mensagens podem ser muito custosas em uma rede lenta, causando excesso de tráfego, o que afeta outros clientes de rede.  
  
 Também é importante esclarecer se você está falando de pipes locais ou pipes de rede. Se o aplicativo de servidor estiver sendo executado localmente no computador que está executando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o protocolo Pipes Nomeados local será uma opção. Os pipes nomeados locais são executados no modo kernel e são muito rápidos.  
  
 Para Soquetes TCP/IP, as transmissões de dados são mais simplificadas e têm menos sobrecarga. As transmissões de dados também podem aproveitar os mecanismos de aprimoramento do desempenho de Soquetes TCP/IP, como janelas, confirmações atrasadas etc. Isso pode ser muito útil em uma rede lenta. Dependendo do tipo de aplicativos, tais diferenças de desempenho podem ser significativas.  
  
 Os Soquetes TCP/IP também dão suporte a uma fila de pendências. Isso pode proporcionar um efeito suavizador limitado em comparação com pipes nomeados que poderiam levar a erros de pipes ocupados quando você tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Em geral, o TCP/IP tem preferência em uma LAN, WAN ou rede de conexão discada lenta, enquanto os pipes nomeados podem ser uma opção melhor quando a velocidade da rede não é o problema, pois ele oferece mais funcionalidade, facilidade de uso e opções de configuração.  
  
## <a name="enabling-the-protocol"></a>Habilitando os protocolos  
 Para funcionar, o protocolo deve ser habilitado no cliente e no servidor. O servidor pode escutar ao mesmo tempo as solicitações em todos os protocolos habilitados. Os computadores cliente podem escolher um ou tentar os protocolos na ordem listada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
 Para obter um breve tutorial sobre como configurar protocolos e conectar-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], confira [: Introdução ao Mecanismo de Banco de Dados.](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
  
