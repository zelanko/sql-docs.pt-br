---
title: Protocolos de Cliente – Propriedades de TCP IP (guia Protocolo)
description: Saiba como especificar as opções de TCP/IP no Microsoft SQL Server Configuration Manager, como o parâmetro keep alive e o número da porta padrão.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: f4b42286216e543c3c2101a140057ed4c4939589
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483828"
---
# <a name="client-protocols---tcp-ip-properties-protocol-tab"></a>Protocolos de Cliente – Propriedades de TCP IP (guia Protocolo)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, use a guia **Protocolo** na caixa de diálogo **Propriedades de TCP/IP** para exibir ou especificar as opções a seguir. Para se conectar a uma porta diferente, digite o número da porta na caixa **Pipe Padrão** . Para obter mais informações sobre cadeias de conexão, consulte [Criando uma cadeia de conexão válida usando TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md).  
  
## <a name="options"></a>Opções  
 **Pipe Padrão**  
 Especifica a porta que a biblioteca de rede TCP/IP usará para tentar se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O valor padrão da porta é 1433.  
  
 Ao conectar a uma instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)], o cliente usa esse valor. Se uma instância padrão tiver sido configurada para escutar em uma porta diferente, altere esse valor para esse número de porta.  
  
 Ao se conectar a uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)], o cliente tentará obter o número da porta no Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no computador servidor. Se o Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, o número da porta deverá ser fornecido por meio dessa configuração, ou como parte da cadeia de conexão.  
  
 **Enabled**  
 Os valores possíveis são **Sim** e **Não**.  
  
 **Keep Alive**  
 Este parâmetro (em milissegundos) controla a frequência das tentativas do TCP de verificar se uma conexão ociosa ainda está intacta enviando um pacote **KEEPALIVE** . O padrão é 30.000 milissegundos.  
  
 **Intervalo de Atividade**  
 Este parâmetro (em milissegundos) determina o intervalo que separa novas transmissões de **KEEPALIVE** até que uma resposta seja recebida. O padrão é 1.000 milissegundos.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))   
 [Novo Alias &#40;Alias Tab&#41;](../../tools/configuration-manager/new-alias-alias-tab.md)   
 [Propriedades &#60;Alias&#62; &#40;Guia Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)  
  
