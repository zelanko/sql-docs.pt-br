---
title: Configurar o Windows para receber cópias de tabelas remotas
description: Descreve como comprar e configurar um sistema Windows que não seja de dispositivo conectado usando a rede InfiniBand para uso com o recurso de cópia de tabela remota em paralelo data warehouse. O sistema Windows hospedará o banco de dados SQL Server que recebe a cópia de tabela remota de um banco de dados SQL Server PDW. Ele é adquirido separadamente do dispositivo e conectado à rede InfiniBand do dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401309"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>Configurar um sistema externo do Windows para receber cópias de tabelas remotas usando o data warehouse de InfiniBand em paralelo
Descreve como comprar e configurar um sistema Windows que não seja de dispositivo conectado usando a rede InfiniBand para uso com o recurso de cópia de tabela remota no SQL Server PDW. O sistema Windows hospedará o banco de dados SQL Server que recebe a cópia de tabela remota de um banco de dados SQL Server PDW. Ele é adquirido separadamente do dispositivo e conectado à rede InfiniBand do dispositivo.  
  
> [!NOTE]  
> Não é necessário conectar-se através da rede InfiniBand para usar a cópia da tabela remota. A conexão por meio da rede Ethernet pode ser feita se a largura de banda da Ethernet atender às suas necessidades.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia de tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Antes de começar  
Antes de configurar o sistema externo do Windows, você deve:  
  
1.  Adquira ou forneça um sistema Windows que receberá as cópias remotas.  
  
2.  Conecte o sistema Windows ao rack de controle (se houver espaço suficiente) ou feche o suficiente para o dispositivo para que você possa conectá-lo à rede InfiniBand do dispositivo.  
  
3.  Compre cabos InfiniBand e um adaptador de rede InfiniBand do fornecedor de hardware do dispositivo. É recomendável comprar um adaptador de rede com duas portas para tolerância a falhas ao receber os dados exportados. Um adaptador de rede de duas portas é recomendado, mas não é um requisito.  
  
## <a name="configure-an-external-windows-system-to-receive-remote-table-copies"></a><a name="HowToWindows"></a>Configurar um sistema Windows externo para receber cópias de tabela remotas  
Para configurar o sistema externo do Windows, use as seguintes etapas:  
  
1.  Instale o adaptador de rede InfiniBand em seu sistema Windows.  
  
2.  Conecte o adaptador de rede InfiniBand ao comutador InfiniBand principal no rack de controle usando cabos InfiniBand.  
  
3.  Instale e configure o driver do Windows apropriado para o adaptador de rede InfiniBand.  
  
    Os drivers InfiniBand para Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio da indústria de fornecedores InfiniBand.  O driver correto pode ter sido distribuído com o adaptador InfiniBand. Caso contrário, o driver pode ser baixado em www.openfabrics.org.  
  
4.  Configure o endereço IP para cada porta no adaptador. Os sistemas SMP são obrigados a usar endereços IP estáticos de um intervalo de endereços reservados para essa finalidade. Configure a primeira porta de acordo com os seguintes parâmetros:  
  
    -   Endereço de rede IP: 172.16.132. x  
  
    -   Máscara de sub-rede IP: 255.255.128.0  
  
    -   Intervalo de host IP: 1-254  
  
    Para adaptadores de rede InfiniBand com duas portas, configure a segunda porta de acordo com os seguintes parâmetros:  
  
    -   Endereço de rede IP: 172.16.132. x  
  
    -   Máscara de sub-rede IP: 255.255.128.0  
  
    -   Intervalo de host IP: 1-254  
  
5.  Se um adaptador de duas portas for usado ou vários sistemas externos do Windows estiverem conectados a um dispositivo, atribua a cada sistema um número de host diferente dentro de cada sub-rede IP.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
